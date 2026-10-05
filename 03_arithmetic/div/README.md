  ## Program 1: div1.asm

### Operation

The program performs:

**100 ÷ 7 = 14 remainder 2**


### Flags

The arithmetic flags are **undefined** after the `DIV` instruction.

* **CF = Undefined:** The `DIV` instruction does not define the Carry Flag. Therefore, the value displayed by GDB cannot be used to determine the result of the division.

* **PF = Undefined:** `DIV` does not define the Parity Flag.

* **AF = Undefined:** `DIV` does not define the Auxiliary Carry Flag.

* **ZF = Undefined:** `DIV` does not define the Zero Flag.

* **SF = Undefined:** `DIV` does not define the Sign Flag.

* **OF = Undefined:** `DIV` does not define the Overflow Flag.



---

## Program 2: div2.asm

### Operation

The program performs:

**50000 ÷ 300 = 166 remainder 200**


### Flags


* **CF = Undefined:** `DIV` does not define the Carry Flag, so its displayed value cannot be used to describe the division result.

* **PF = Undefined:** `DIV` does not define the Parity Flag.

* **AF = Undefined:** `DIV` does not define the Auxiliary Carry Flag.

* **ZF = Undefined:** `DIV` does not define the Zero Flag.

* **SF = Undefined:** `DIV` does not define the Sign Flag.

* **OF = Undefined:** `DIV` does not define the Overflow Flag.


