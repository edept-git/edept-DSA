### Description
You are given an array of integers `tasks` representing the complexity or size of `n` tasks, and an integer `k` representing the number of workers available. Your goal is to assign all tasks to these `k` workers. The tasks must be assigned contiguously, meaning if `tasks` is split into `k` contiguous segments, each segment is assigned to one worker. You need to find a way to assign tasks such that the maximum total complexity assigned to any single worker is minimized. Return this minimum possible maximum complexity.

### Constraints
- `1 <= n (length of tasks) <= 10^5`
- `1 <= tasks[i] <= 10^9`
- `1 <= k <= n`
- The sum of `tasks` can exceed `2^31 - 1`, so use 64-bit integers for sums where applicable.

### Example
Input:
tasks = [10, 20, 30, 40]
k = 2
Output:
60
Explanation:
Possible distributions:
1. Worker 1: [10], Worker 2: [20, 30, 40] -> Max load = 90
2. Worker 1: [10, 20], Worker 2: [30, 40] -> Max load = 70
3. Worker 1: [10, 20, 30], Worker 2: [40] -> Max load = 60
The minimum among these maximum loads is 60.

### Concepts Covered
- Binary Search
- Predicate Function (or Check Function)
- Search Space Definition (Lower Bound, Upper Bound)