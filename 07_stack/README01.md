# Program 01 

## Stack Execution

1. **Program starts:** RSP initially points to `0x7fffffffd9c0`. The stack contains existing startup data, and the registers used in the program are initially zero.
2. **Loading values:** `mov rax, 100` and `mov rbx, 200` load values into RAX and RBX. These instructions do not affect the stack or change RSP.
3. **First PUSH:** `push rax` places 100 onto the stack. RSP decreases by 8 bytes because the stack grows towards lower memory addresses.
4. **Second PUSH:** `push rbx` places 200 onto the stack. RSP decreases by another 8 bytes. The value 200 is now at the top of the stack, above 100.
5. **NOP instruction:** `nop` performs no operation and does not affect the stack.
6. **First POP:** `pop rcx` retrieves 200 from the top of the stack and stores it in RCX. RSP increases by 8 bytes.
7. **Second POP:** `pop rdx` retrieves 100 and stores it in RDX. RSP increases by another 8 bytes, returning to its original value.
8. **Program ends:** Both values have been retrieved successfully, and the stack pointer is restored to its initial position.

## Stack Observations

- The stack grows downward, towards lower memory addresses.
- Each `PUSH` decreases RSP by 8 bytes in 64-bit mode.
- Each `POP` increases RSP by 8 bytes.
- Values are retrieved in LIFO (Last In, First Out) order.
- The `MOV` and `NOP` instructions do not affect the stack.
- Popped values may still physically remain in memory, but they are no longer considered part of the active stack.
- The two PUSH operations and two POP operations restore RSP to its original position.