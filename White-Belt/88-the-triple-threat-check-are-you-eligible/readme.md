### Description
You are given two integers, `num1` and `num2`. Your task is to determine if both numbers collectively satisfy a specific set of criteria. You need to combine the results of several individual checks using logical operators.

The conditions are:
1.  `num1` must be an even number.
2.  `num2` must be a positive number (strictly greater than 0).
3.  The sum of `num1` and `num2` must be strictly less than 50.
4.  The product of `num1` and `num2` must be strictly greater than 0.

If all four conditions are met, your function should return `true`. Otherwise, it should return `false`.

### Constraints
*   `num1` and `num2` will be integers.
*   `-100 <= num1, num2 <= 100`

### Example
**Input:**

10
5


**Output:**

true


**Explanation:**
1.  `num1` (10) is even. (`10 % 2 == 0` is `true`)
2.  `num2` (5) is positive. (`5 > 0` is `true`)
3.  The sum `10 + 5 = 15`, which is less than 50. (`15 < 50` is `true`)
4.  The product `10 * 5 = 50`, which is greater than 0. (`50 > 0` is `true`)
Since all conditions are `true`, the function returns `true`.

### Concepts Covered
*   **Arithmetic Operators:** Addition (`+`), Multiplication (`*`), Modulo (`%`)
*   **Relational Operators:** Equality (`==`), Greater Than (`>`), Less Than (`<`)
*   **Logical Operators:** Logical AND (`&&` or `and`)