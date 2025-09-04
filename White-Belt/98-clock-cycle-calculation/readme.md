### Description
Imagine a standard 12-hour clock. You are given the current hour and a certain number of hours that have passed. Your task is to determine what hour it will be after those hours have elapsed. Remember that a 12-hour clock cycles from 1 to 12.

For example, if it's 3 o'clock and 5 hours pass, it will be 8 o'clock. If it's 10 o'clock and 4 hours pass, it will be 2 o'clock (because 10 + 4 = 14, and on a 12-hour clock, 14 hours past 12 is 2).

### Constraints
*   `1 <= startHour <= 12` (The starting hour is between 1 and 12, inclusive)
*   `0 <= hoursPassed <= 1000` (The number of hours passed is non-negative)

### Example
**Input:**

startHour = 10
hoursPassed = 4


**Output:**

2


**Explanation:**
Starting at 10 o'clock, after 4 hours, it would be 10 + 4 = 14. On a 12-hour clock, 14 hours is equivalent to 2 o'clock (since 14 - 12 = 2).

### Concepts Covered
*   Modulo Operator
*   Basic Arithmetic Operations