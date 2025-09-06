### Description
You are given an array of integers, `arr`, and a list of queries. Each query consists of two indices, `start` and `end`, representing a range within the array (inclusive). Your task is to calculate the sum of all elements within each specified range for every query.

For example, if `arr = [1, 2, 3, 4, 5]` and a query is `[0, 2]`, the sum would be `arr[0] + arr[1] + arr[2] = 1 + 2 + 3 = 6`. You need to process all queries efficiently.

### Constraints
- `1 <= N <= 10^5` (where `N` is the length of `arr`)
- `-1000 <= arr[i] <= 1000`
- `1 <= Q <= 10^5` (where `Q` is the number of queries)
- `0 <= start <= end < N` for each query

### Example
Input:
Array: `[1, 2, 3, 4, 5]`
Queries: `[[0, 2], [1, 3]]`

Output:
`[6, 9]`

Explanation:
For the first query `[0, 2]`: `arr[0] + arr[1] + arr[2] = 1 + 2 + 3 = 6`
For the second query `[1, 3]`: `arr[1] + arr[2] + arr[3] = 2 + 3 + 4 = 9`

### Concepts Covered
- Prefix Sums
- Array Manipulation
- Time and Space Complexity Analysis
