### Description
You are given a starting day of the week (represented by a number from 0 for Monday to 6 for Sunday) and a number of days that have passed. Your task is to calculate and return the day of the week it will be after those days have passed.

For example, if today is Wednesday (day 2) and 3 days pass, it will be Saturday (day 5).
If today is Friday (day 4) and 4 days pass, it will be Tuesday (day 1).

### Constraints
*   `0 <= startDay <= 6` (representing Monday to Sunday)
*   `0 <= daysPassed <= 1000`

### Example
#### Input:

2
5

(startDay = 2, daysPassed = 5)

#### Output:

0


Explanation: If today is Wednesday (day 2) and 5 days pass:
Wednesday (2) + 1 day = Thursday (3)
Thursday (3) + 1 day = Friday (4)
Friday (4) + 1 day = Saturday (5)
Saturday (5) + 1 day = Sunday (6)
Sunday (6) + 1 day = Monday (0)
So, `(2 + 5) % 7 = 7 % 7 = 0`. The resulting day is Monday.

### Concepts Covered
*   Modulo Arithmetic
*   Integer Arithmetic