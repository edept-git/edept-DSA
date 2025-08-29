### Description
You are given an integer `A` and a double-precision floating-point number `B`. Your task is to perform specific type conversions and calculations:

1.  **Integer to Double:** Convert integer `A` to a `double` and store it in a new variable, say `double_A`.
2.  **Double to Integer:** Convert double `B` to an `integer` (truncating any decimal part) and store it in a new variable, say `int_B`.
3.  **Double Sum:** Calculate the sum of `double_A` (the converted `A`) and the original `double B`. Store this in `double_sum`.
4.  **Integer Sum:** Calculate the sum of the original `integer A` and `int_B` (the converted `B`). Store this in `int_sum`.

Finally, print the four resulting values (`double_A`, `int_B`, `double_sum`, `int_sum`) in the order specified, each on a new line. Floating-point numbers should be printed with two decimal places.

### Constraints
- `-1000 <= A <= 1000`
- `-1000.0 <= B <= 1000.0`
- Input will consist of a single line with `A` followed by `B`, separated by a space.

### Example
Input: `10 5.75`
Output:

10.00
5
15.75
15


### Concepts Covered
- Type Casting (explicit and implicit)
- Integer data types
- Floating-point data types (specifically `double`)
- Basic arithmetic operations
- Input/Output handling