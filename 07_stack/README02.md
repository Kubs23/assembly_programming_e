# Program 02 

## Stack Execution

1. **Program starts:** RSP initially points to `0x7fffffffd9c0`. RBP is initially 0, and the other registers are zero.

2. **CALL instruction:** `call work` pushes the return address (`0x401005`) onto the stack and transfers execution to the `work` subroutine. RSP decreases by 8 bytes to `0x7fffffffd9b8`.

3. **Saving RBP:** `push rbp` saves the previous RBP value (0) onto the stack. RSP decreases by another 8 bytes to `0x7fffffffd9b0`.

4. **Setting the frame pointer:** `mov rbp, rsp` copies the current RSP value into RBP. RBP now points to the base of the new stack frame.

5. **Allocating local variables:** `sub rsp, 16` reserves 16 bytes of stack memory for two local variables. RSP decreases to `0x7fffffffd9a0`.

6. **Storing local variables:** 
   - `mov qword [rbp-8], 100` stores 100 at address `0x7fffffffd9a8`.
   - `mov qword [rbp-16], 200` stores 200 at address `0x7fffffffd9a0`.

   These instructions do not change RSP because memory is accessed using offsets from RBP.

7. **Reading local variables:** `mov rax, [rbp-8]` loads 100 into RAX, while `mov rbx, [rbp-16]` loads 200 into RBX. RSP remains unchanged.

8. **NOP instruction:** `nop` performs no operation and does not affect the stack.

9. **Releasing the stack frame:** `mov rsp, rbp` restores RSP to `0x7fffffffd9b0`, releasing the 16 bytes reserved for local variables.

10. **Restoring RBP:** `pop rbp` retrieves the previously saved RBP value (0). RSP increases by 8 bytes to `0x7fffffffd9b8`.

11. **Returning from the subroutine:** `ret` retrieves the return address and transfers execution back to the instruction after the original `call`. RSP increases by 8 bytes to `0x7fffffffd9c0`.

12. **Program ends:** The stack pointer returns to its original position, and the subroutine has completed successfully.

## Stack Observations

- The `CALL` instruction pushes a return address onto the stack, while `RET` retrieves it.
- The stack grows downward towards lower memory addresses.
- `PUSH RBP` saves the previous frame pointer before creating a new stack frame.
- `MOV RBP, RSP` establishes a fixed reference point for accessing local variables.
- `SUB RSP, 16` reserves 16 bytes for the two local variables.
- Local variables are accessed using offsets from RBP rather than being individually pushed onto the stack.
- `MOV RSP, RBP` releases the allocated local memory in one instruction.
- The epilogue restores the previous RBP and returns execution to the caller.
- After the subroutine returns, RSP is restored to its original value.