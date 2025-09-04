### Description
Given an integer array `nums` that contains distinct elements, return all possible subsets (the power set). The solution set must not contain duplicate subsets. The order of subsets and the order of elements within a subset can be arbitrary.

### Constraints
- `0 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the elements of `nums` are unique.

### Example
Input: `nums = [1,2,3]`
Output:

[]
[1]
[1 2]
[1 2 3]
[1 3]
[2]
[2 3]
[3]

(The order of subsets and elements within subsets shown above is just one possible valid output based on the provided solution.)

### Concepts Covered
-   **Backtracking:** A general algorithm for finding all (or some) solutions to computational problems, that incrementally builds candidates to the solutions, and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.
-   **Recursion:** A function calling itself to solve smaller instances of the same problem.
-   **Power Set:** The set of all possible subsets of a given set, including the empty set and the set itself.
