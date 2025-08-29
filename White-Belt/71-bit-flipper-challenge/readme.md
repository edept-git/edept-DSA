### Description
You are given an integer `num` and a non-negative integer `n`. Your task is to toggle (flip) the `n`-th bit of `num` and return the new integer. The `n`-th bit is 0-indexed, meaning the 0-th bit is the rightmost (least significant) bit.

### Constraints
*   `0 <= num <= 10^9`
*   `0 <= n <= 30`

### Example
**Input:**

num = 4
n = 1


**Explanation:**
1.  The decimal number `4` in binary is `...0100`.
2.  The `n`-th bit is the 1st bit (0-indexed). In `...0100`, the 1st bit is currently `0`.
3.  To toggle this bit means to flip its value from `0` to `1`.
4.  After flipping, the binary representation becomes `...0110`.
5.  The binary `...0110` is `6` in decimal.

**Output:**

6


### Concepts Covered
*   Bitwise XOR (`^`)
*   Left Shift Operator (`<<`)
*   Binary Representation of Integers
*   0-indexed bit positions