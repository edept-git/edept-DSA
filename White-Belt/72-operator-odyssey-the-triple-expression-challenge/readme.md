### Description
You are given three integers: `num1`, `num2`, and `num3`. Your task is to perform two distinct calculations and print their results.

1.  **Arithmetic Calculation**: Calculate the value of `(num1 + num2) * num3`.
2.  **Logical Calculation**: Evaluate the boolean expression `(num1 > num2) && (num2 < num3)`.

Print the result of the arithmetic calculation on the first line, and the result of the logical calculation (as `true` or `false` or their equivalent in the respective language, e.g., `1` or `0` for C/C++, `True` or `False` for Python) on the second line.

### Constraints
- `1 <= num1, num2, num3 <= 1000`

### Example
#### Input:

10
5
20

#### Output:

300
true

#### Explanation:
1.  Arithmetic: `(10 + 5) * 20 = 15 * 20 = 300`
2.  Logical: `(10 > 5) && (5 < 20)` evaluates to `true && true`, which is `true`.

### Concepts Covered
-   **Arithmetic Operators**: Addition (`+`), Multiplication (`*`)
-   **Relational Operators**: Greater than (`>`), Less than (`<`)
-   **Logical Operators**: Logical AND (`&&`)
-   Basic input/output operations
-   Integer and Boolean data types