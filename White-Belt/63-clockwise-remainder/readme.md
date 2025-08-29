### Description
Imagine a 24-hour clock. Given the current hour and a number of hours that will pass, your task is to determine what the hour will be after the duration has passed. The clock operates from 0 to 23 (e.g., 0 is midnight, 13 is 1 PM, 23 is 11 PM).

### Constraints
*   `0 <= current_hour <= 23`
*   `0 <= duration_hours <= 1000`
*   The final hour should also be between 0 and 23.

### Example
**Input:**

10
5

This means `current_hour = 10` and `duration_hours = 5`.

**Output:**

15

Explanation: `10 + 5 = 15`. Since `15` is within `0-23`, it's the final hour.

**Input:**

20
8

This means `current_hour = 20` and `duration_hours = 8`.

**Output:**

4

Explanation: `20 + 8 = 28`. On a 24-hour clock, `28` hours past `0` is equivalent to `4` hours (`28 % 24 = 4`).

### Concepts Covered
*   Modulo Arithmetic