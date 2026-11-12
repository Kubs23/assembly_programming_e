# Program 04 

## Stack Execution

1. **Program starts:** ESP initially points to `0xffffcb30`. EBP, EAX, EBX, ECX and EDX are initially zero. The stack also contains existing startup data.

2. **CALL instruction:** `call work` pushes the return address (`0x8049005`) onto the stack and transfers execution to the `work` subroutine. ESP decreases by 4 bytes to `0xffffcb2c`.

3. **Saving EBP:** `push %ebp` saves the previous EBP value (0) onto the stack. ESP decreases by another 4 bytes to `0xffffcb28`.

4. **Setting the frame pointer:** `mov %esp, %ebp` copies the current ESP value into EBP. EBP now points to the base of the new stack frame.

5. **Allocating local variables:** `sub $0x8, %esp` reserves 8 bytes of stack memory for two 4-byte local variables. ESP decreases to `0xffffcb20`.

6. **Storing local variables:**
   - `movl $0x64, -0x4(%ebp)` stores 100 at address `0xffffcb24`.
   - `movl $0xc8, -0x8(%ebp)` stores 200 at address `0xffffcb20`.

   These instructions do not change ESP because the memory locations are accessed using offsets from EBP.

7. **Reading local variables:** `mov -0x4(%ebp), %eax` loads 100 into EAX, while `mov -0x8(%ebp), %ebx` loads 200 into EBX. ESP remains unchanged.

8. **NOP instruction:** `nop` performs no operation and does not affect the stack.

9. **Releasing the stack frame:** `mov %ebp, %esp` restores ESP to `0xffffcb28`, releasing the 8 bytes reserved for local variables.

10. **Restoring EBP:** `pop %ebp` retrieves the previously saved EBP value (0). ESP increases by 4 bytes to `0xffffcb2c`.

11. **Returning from the subroutine:** `ret` retrieves the return address and transfers execution back to the instruction after the original `CALL`. ESP increases by another 4 bytes to `0xffffcb30`.

12. **Program ends:** `mov $0x1, %eax` sets the exit system call number, `xor %ebx, %ebx` sets the exit status to 0, and `int $0x80` invokes the kernel to terminate the program.

## Stack Observations

- The stack grows downward towards lower memory addresses.
- Each PUSH and POP operation moves ESP by 4 bytes in 32-bit mode.
- The `CALL` instruction pushes a return address, while `RET` retrieves it.
- `PUSH EBP` saves the previous frame pointer before creating a new stack frame.
- `MOV EBP, ESP` establishes a reference point for accessing local variables.
- `SUB ESP, 8` reserves 8 bytes for the two local variables.
- Local variables are accessed using offsets from EBP rather than being individually pushed onto the stack.
- `MOV ESP, EBP` releases the allocated local memory in one instruction.
- The epilogue restores the previous EBP and returns execution to the caller.
- After `RET`, ESP returns to its original value of `0xffffcb30`.
- The program exits successfully with status 0 using the 32-bit `int 0x80` system call.