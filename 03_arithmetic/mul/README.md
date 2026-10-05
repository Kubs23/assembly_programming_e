## Program 1: mul1.asm

### Operation

The program performs:

**25 × 10 = 250**


### Flags

* **CF = 0 (Cleared):** The upper half of the 16-bit result is zero. Since `AX = 0x00FA`, the upper byte `AH = 0x00`. Therefore, CF is cleared.

* **OF = 0 (Cleared):** The upper half of the product is zero, meaning the result fits completely within the original 8-bit operand size. Therefore, OF is cleared.

* **PF = Undefined:** `MUL` does not define the Parity Flag. The value displayed by GDB should not be interpreted as a meaningful result of the multiplication.

* **AF = Undefined:** `MUL` does not define the Auxiliary Carry Flag.

* **ZF = Undefined:** `MUL` does not define the Zero Flag.

* **SF = Undefined:** `MUL` does not define the Sign Flag.


---

## Program 2: mul2.asm

### Operation

The program performs:

**3000 × 200 = 600000**


### Flags

For the `MUL` instruction, only **CF** and **OF** are defined. The other arithmetic flags are undefined.

* **CF = 1 (Set):** The upper 16 bits of the product are stored in `DX`. Since `DX = 0x0009`, the upper half is nonzero. Therefore, CF is set.

* **OF = 1 (Set):** The upper half of the product is nonzero, so the product does not fit completely within 16 bits. Therefore, OF is set.

* **PF = Undefined:** `MUL` does not define the Parity Flag, so the value displayed by GDB is not meaningful for this instruction.

* **AF = Undefined:** `MUL` does not define the Auxiliary Carry Flag.

* **ZF = Undefined:** `MUL` does not define the Zero Flag.

* **SF = Undefined:** `MUL` does not define the Sign Flag.


