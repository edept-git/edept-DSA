### Description

You're the commander of a data analysis unit, and your team has collected a long sequence of numbers. You need to process various queries asking for the sum of elements within specific ranges (segments) of this sequence. A naive approach of summing elements for each query would be too slow given the potentially large number of queries and the sequence length. Your mission is to implement an efficient system that can quickly respond to these range sum queries.

Given an array of `n` integers and `q` queries, each query consists of two indices, `L` and `R` (0-indexed). For each query, you must find the sum of all elements in the array from index `L` to `R`, inclusive.

### Constraints

*   `1 <= n <= 10^5` (size of the array)
*   `1 <= q <= 10^5` (number of queries)
*   `-10^9 <= arr[i] <= 10^9` (value of array elements)
*   `0 <= L <= R < n` (query indices are valid)
*   The sum of elements in a range can exceed the capacity of a 32-bit integer, so use a 64-bit integer type (e.g., `long long` in C++/C, `long` in Java, standard integers in Python/JS).

### Example

**Input:**

5
1 2 3 4 5
2
0 2
2 4


**Output:**

6
12


**Explanation:**
*   For the array `[1, 2, 3, 4, 5]`
*   Query `(0, 2)`: `arr[0] + arr[1] + arr[2] = 1 + 2 + 3 = 6`
*   Query `(2, 4)`: `arr[2] + arr[3] + arr[4] = 3 + 4 + 5 = 12`

### Concepts Covered

*   Arrays
*   Prefix Sums (Cumulative Sums)
*   Time Complexity Optimization
*   Basic I/O
