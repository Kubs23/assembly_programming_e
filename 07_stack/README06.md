# Program 06 

## Stack Execution

1. **Program starts:** ESP initially points to `0xffffcb30`. EBP and the general-purpose registers are initially zero. The stack contains existing startup data.

2. **Loading the first value:** `mov $0x11223344, %eax` loads `0x11223344` into EAX. The stack remains unchanged.

3. **Loading the second value:** `mov $0x1234, %ebx` loads `0x1234` into EBX. ESP remains unchanged.

4. **First PUSH:** `push %eax` places `0x11223344` onto the stack. ESP decreases by 4 bytes to `0xffffcb2c`.

5. **Second PUSH:** `push %ebx` places `0x00001234` onto the stack. ESP decreases by another 4 bytes to `0xffffcb28`. The value `0x1234` is now at the top of the stack.

6. **NOP instruction:** `nop` performs no operation and does not affect the stack.

7. **First POP:** `pop %ebx` retrieves `0x1234` from the top of the stack and stores it in EBX. ESP increases by 4 bytes to `0xffffcb2c`.

8. **Second POP:** `pop %eax` retrieves `0x11223344` and stores it in EAX. ESP increases by another 4 bytes, returning to `0xffffcb30`.

9. **Program ends:** `mov $0x1, %eax` sets the exit system call number, `xor %ebx, %ebx` sets the exit status to 0, and `int $0x80` invokes the kernel to terminate the program. These instructions do not affect the stack.

## Stack Observations

- The stack grows downward towards lower memory addresses.
- Each PUSH decreases ESP by 4 bytes in 32-bit mode.
- Each POP increases ESP by 4 bytes.
- Values are retrieved in LIFO (Last In, First Out) order.
- The value `0x1234` is retrieved first because it was pushed last.
- The `MOV` instructions do not affect the stack.
- After two PUSH operations and two POP operations, ESP returns to its original value.
- Compared to Program 05, which uses 16 bytes for two pushes, this program uses only 8 bytes.
- The stack operation size depends on the architecture: 8 bytes in 64-bit mode and 4 bytes in 32-bit mode.