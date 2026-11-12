# Program 05

## Stack Execution

1. **Program starts:** RSP initially points to `0x7fffffffd9c0`. RBP and the general-purpose registers are initially zero. The stack contains existing startup data.

2. **Loading the first value:** `movabs $0x1122334455667788, %rax` loads the 64-bit value into RAX. The stack remains unchanged.

3. **Loading the second value:** `mov $0x1234, %ebx` loads `0x1234` into RBX. The upper 32 bits are automatically cleared because the instruction writes to EBX. RSP remains unchanged.

4. **First PUSH:** `push %rax` places `0x1122334455667788` onto the stack. RSP decreases by 8 bytes to `0x7fffffffd9b8`.

5. **Second PUSH:** `push %rbx` places `0x0000000000001234` onto the stack. Even though the value was loaded through EBX, PUSH stores a full 8-byte value. RSP decreases by another 8 bytes to `0x7fffffffd9b0`.

6. **NOP instruction:** `nop` performs no operation and does not affect the stack.

7. **First POP:** `pop %rbx` retrieves `0x1234` from the top of the stack and stores it in RBX. RSP increases by 8 bytes to `0x7fffffffd9b8`.

8. **Second POP:** `pop %rax` retrieves `0x1122334455667788` and stores it in RAX. RSP increases by another 8 bytes, returning to `0x7fffffffd9c0`.

9. **Program ends:** `mov $0x3c, %eax` sets the exit system call number, `xor %rdi, %rdi` sets the exit status to 0, and `syscall` terminates the program. These instructions do not affect the stack.

## Stack Observations

- The stack grows downward towards lower memory addresses.
- Each PUSH decreases RSP by 8 bytes in 64-bit mode.
- Each POP increases RSP by 8 bytes.
- PUSH stores a full 8-byte value in this 64-bit program.
- Writing to EBX automatically clears the upper 32 bits of RBX.
- Values are retrieved in LIFO (Last In, First Out) order.
- The smaller value (`0x1234`) is retrieved first because it was pushed last.
- The two PUSH operations and two POP operations restore RSP to its original value.
- Compared to Program 01, the stack operations are identical, but larger hexadecimal values make the stored memory contents easier to distinguish.