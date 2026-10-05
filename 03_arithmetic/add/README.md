## Program 1: add1.asm

### Operation

The program performs:

**120 + 10 = 130**


### Flags

* **CF = 0 (Cleared):** 130 fits within the 8-bit unsigned range of 0–255, so there is no carry out of bit 7.

* **PF = 1 (Set):** The result `10000010` contains two 1-bits. Since the number of 1-bits is even, PF is set.

* **AF = 1 (Set):** Adding the lower nibbles causes a carry from bit 3 to bit 4, so AF is set.

* **ZF = 0 (Cleared):** The result is 130, which is not zero.

* **SF = 1 (Set):** The most significant bit of the 8-bit result is 1.

* **OF = 1 (Set):** The signed 8-bit range is −128 to +127. The result 130 is outside this range, so signed overflow occurs.


---

## Program 2: add2.asm

### Operation

The program performs:

**32000 + 500 = 32500**


### Flags

* **CF = 0 (Cleared):** 32500 fits within the unsigned 16-bit range of 0–65535, so there is no carry out of bit 15.

* **PF = 0 (Cleared):** The low byte is `F4`, which is `11110100` in binary. It contains five 1-bits. Since five is odd, PF is cleared.

* **AF = 0 (Cleared):** The lower nibbles do not produce a carry from bit 3 to bit 4.

* **ZF = 0 (Cleared):** The result 32500 is not zero.

* **SF = 0 (Cleared):** The most significant bit of the 16-bit result is 0, so the result is positive.

* **OF = 0 (Cleared):** 32500 is within the signed 16-bit range of −32768 to +32767, so signed overflow does not occur.
