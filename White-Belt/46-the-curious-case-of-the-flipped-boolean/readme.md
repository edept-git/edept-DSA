### Description

Given two integer inputs, `a` and `b`, determine if the following conditions are met simultaneously:

1. `a` is greater than 10.
2. `b` is less than or equal to 5.
3.  The logical AND of (`a` > 10) and (`b` <= 5) is true, but the logical OR of those same conditions is false.  This is a trick to check for understanding of logical operators.

Your program should output `true` if all three conditions are true; otherwise, output `false`.

### Constraints

-100 ≤ a ≤ 100
-100 ≤ b ≤ 100

### Example

Input: 15 3
Output: false

Input: 20 5
Output: false

Input: 12 2
Output: false

### Concepts Covered

Arithmetic operators (+, -, *, /, %), Relational operators (>, <, >=, <=, ==, !=), Logical operators (&&, ||, !)