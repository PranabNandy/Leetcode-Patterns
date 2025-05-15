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

