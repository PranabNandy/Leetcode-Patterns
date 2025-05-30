# 0.JoiBabaSaiNath
## Question 1:

In a resource-constrained embedded system (e.g., a microcontroller with limited RAM and no dynamic memory allocation), implement a fixed-size circular buffer to store incoming bytes from a UART peripheral.

**The buffer must support:**
- push(uint8_t byte): add a byte to the buffer (return error if full).
- pop(uint8_t* byte): remove a byte from the buffer (return error if empty).
- is_full(), is_empty()

**The implementation should be:**

- Interrupt-safe (assume push is called from ISR, and pop is called from main loop).

- Lock-free and without dynamic memory allocation.

**Constraints:**

- Use a buffer size of 128 bytes.

- Use only fixed-size types (uint8_t, uint16_t, etc.).

- Must avoid buffer overflow or underflow.

- No use of STL or malloc.

**Follow-up:**

- What happens if the producer is faster than the consumer?

- How would you modify the design to support multiple producers or consumers?

```c++
#include <stdint.h>
#include <stdbool.h>

#define BUFFER_SIZE 128

typedef struct {
    uint8_t buffer[BUFFER_SIZE];
    volatile uint16_t head; // Points to where to write next
    volatile uint16_t tail; // Points to where to read next
} CircularBuffer;

void cb_init(CircularBuffer *cb) {
    cb->head = 0;
    cb->tail = 0;
}

bool cb_is_full(CircularBuffer *cb) {
    return ((cb->head + 1) % BUFFER_SIZE) == cb->tail;
}

bool cb_is_empty(CircularBuffer *cb) {
    return cb->head == cb->tail;
}

// Called from ISR
bool cb_push(CircularBuffer *cb, uint8_t byte) {
    uint16_t next = (cb->head + 1) % BUFFER_SIZE;
    if (next == cb->tail) {
        // Buffer is full
        return false;
    }
    cb->buffer[cb->head] = byte;
    cb->head = next;
    return true;
}

// Called from main loop
bool cb_pop(CircularBuffer *cb, uint8_t *byte) {
    if (cb_is_empty(cb)) {
        return false;
    }
    *byte = cb->buffer[cb->tail];
    cb->tail = (cb->tail + 1) % BUFFER_SIZE;
    return true;
}
```

### 1. What happens if the producer is faster than the consumer?
The buffer fills up, and push() starts returning false (overflow condition).

Possible consequences: data loss (e.g., UART RX bytes dropped).

### 3. How would you handle wraparound efficiently without modulo?
Replace modulo with bitwise AND if BUFFER_SIZE is power of 2:

```c
#define BUFFER_MASK (BUFFER_SIZE - 1)
next = (cb->head + 1) & BUFFER_MASK;
```
## Question 2:
You're developing firmware for an ARM Cortex-M microcontroller running FreeRTOS. You need to handle high-speed UART input using DMA and store it in a lock-free circular buffer for the application layer to consume safely.

✅ C++ UART Circular Buffer with DMA Integration

```cpp
#ifndef CIRCULARBUFFER_HPP
#define CIRCULARBUFFER_HPP

#include <cstdint>
#include <atomic>

template<size_t Size>
class CircularBuffer {
    static_assert((Size & (Size - 1)) == 0, "Size must be power of 2");

public:
    CircularBuffer() : head(0), tail(0) {}

    bool push(uint8_t data) {
        size_t next = (head + 1) & (Size - 1);
        if (next == tail.load(std::memory_order_acquire)) {
            return false; // Buffer full
        }
        buffer[head] = data;
        head = next;
        return true;
    }

    bool pop(uint8_t& data) {
        size_t t = tail.load(std::memory_order_relaxed);
        if (head == t) return false; // Buffer empty
        data = buffer[t];
        tail.store((t + 1) & (Size - 1), std::memory_order_release);
        return true;
    }

    bool is_empty() const {
        return head == tail.load();
    }

    bool is_full() const {
        return ((head + 1) & (Size - 1)) == tail.load();
    }

private:
    uint8_t buffer[Size];
    size_t head;
    std::atomic<size_t> tail;
};
#endif
```
🧩 Integration with UART + DMA + FreeRTOS
UART RX DMA Half/Full Callback
In your stm32xx_hal_uart.c or similar:

c
Copy
Edit
void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart) {
    BaseType_t xHigherPriorityTaskWoken = pdFALSE;
    // Notify task to copy DMA buffer to circular buffer
    vTaskNotifyGiveFromISR(uartTaskHandle, &xHigherPriorityTaskWoken);
    portYIELD_FROM_ISR(xHigherPriorityTaskWoken);
}
FreeRTOS Task to Transfer from DMA Buffer to CircularBuffer
cpp
Copy
Edit
extern CircularBuffer<256> uartRxBuffer;
extern uint8_t dmaRxBuffer[64]; // DMA buffer

void UARTProcessingTask(void *pvParameters) {
    for (;;) {
        ulTaskNotifyTake(pdTRUE, portMAX_DELAY); // Wait for notification
        for (int i = 0; i < 64; ++i) {
            uartRxBuffer.push(dmaRxBuffer[i]); // Push into circular buffer
        }
    }
}
