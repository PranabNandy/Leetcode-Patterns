## Packed struct
On ARM Cortex-M (32-bit), alignment rules are usually:

- short int (2 bytes) → aligned to 2 bytes

- float (4 bytes) → aligned to 4 bytes
```c++
struct temperature_data {
    short int min;   // offset 0–1
                     // +2 bytes padding (to align next field on 4-byte boundary)
    short int max;   // offset 4–5
                     // +2 bytes padding
    float reading;   // offset 8–11
}; // total size = 12 bytes
```

## Unpacked struct
```c++
struct temperature_data {
    short int min;   // offset 0–1
    short int max;   // offset 2–3
    float reading;   // offset 4–7
}; // total size = 8 bytes

```


