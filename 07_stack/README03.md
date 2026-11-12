# Program 03 

## Stack Execution

1. **Program starts:** RSP initially points to `0x7fffffffd9c0`. RBP is initially 0, and the other registers are zero.

2. **Loading a value:** `mov $0xa, %eax` loads 10 into RAX. The stack remains unchanged, and RSP stays at `0x7fffffffd9c0`.

3. **CALL instruction:** `call calculate` pushes the return address (`0x40100a`) onto the stack and transfers execution to the `calculate` subroutine. RSP decreases by 8 bytes to `0x7fffffffd9b8`.

4. **Executing the subroutine:** `add $0x5, %rax` adds 5 to RAX, changing its value from 10 to 15. The instruction does not affect the stack because the subroutine uses a register instead of local stack memory.

5. **RET instruction:** `ret` retrieves the return address from the stack and transfers execution back to the instruction after the original `CALL`. RSP increases by 8 bytes, returning to `0x7fffffffd9c0`.

6. **NOP instruction:** `nop` performs no operation and does not affect the stack.

7. **Preparing to exit:** `mov $0x3c, %eax` sets the system call number for exit, while `xor %rdi, %rdi` sets the exit status to 0. These instructions do not affect the stack.

8. **Program ends:** `syscall` executes the exit operation. The program terminates successfully with exit status 0.

## Stack Observations

- The `CALL` instruction pushes the return address onto the stack, decreasing RSP by 8 bytes.
- The `RET` instruction retrieves the return address, increasing RSP by 8 bytes.
- The stack grows downward towards lower memory addresses.
- No stack frame is created because the subroutine does not use local variables.
- The subroutine performs its calculation using RAX without accessing stack memory.
- `CALL` and `RET` are the only instructions in this program that change RSP.
- After `RET`, RSP returns to its original value of `0x7fffffffd9c0`.
- Unlike Program 02, this program does not need a prologue or epilogue because it has no local variables to manage.