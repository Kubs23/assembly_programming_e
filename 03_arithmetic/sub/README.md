## Program 1: sub1.asm

### Operation

The program performs:

**50 − 80 = −30**

### Flags

* **CF = 1 (Set):** For unsigned arithmetic, 50 is smaller than 80, so a borrow is required. Therefore, CF is set.

* **PF = 1 (Set):** The result `11100010` contains four 1-bits. Since four is even, PF is set.

* **AF = 0 (Cleared):** The lower nibble of 50 is `0`, and the lower nibble of 80 is also `0`. The subtraction does not require a borrow from bit 4, so AF is cleared.

* **ZF = 0 (Cleared):** The result is `0xE2`, which is not zero.

* **SF = 1 (Set):** The most significant bit of the 8-bit result is 1, indicating a negative result in signed representation.

* **OF = 0 (Cleared):** The signed result −30 is within the signed 8-bit range of −128 to +127, so signed overflow does not occur.


---

## Program 2: sub2.asm

### Operation

The program performs:

**1000 − 2000 = −1000**

### Flags

* **CF = 1 (Set):** For unsigned arithmetic, 1000 is smaller than 2000, so a borrow is required. Therefore, CF is set.

* **PF = 1 (Set):** The low byte of `0xFC18` is `0x18`, which is `00011000` in binary. It contains two 1-bits. Since two is even, PF is set.

* **AF = 0 (Cleared):** The lower nibble of 1000 is `0`, and the lower nibble of 2000 is also `0`. No borrow is required from bit 4, so AF is cleared.

* **ZF = 0 (Cleared):** The result `0xFC18` is not zero.

* **SF = 1 (Set):** The most significant bit of the 16-bit result is 1, indicating a negative signed result.

* **OF = 0 (Cleared):** The signed result −1000 is within the signed 16-bit range of −32768 to +32767, so signed overflow does not occur.

