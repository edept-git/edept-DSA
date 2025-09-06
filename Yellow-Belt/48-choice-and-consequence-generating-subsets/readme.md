### Description
Given an array of unique integers `nums`, the task is to return all possible subsets (the power set). The solution set must not contain duplicate subsets.

The order of the subsets and the order of elements within each subset does not matter, but your output should be consistent.

### Constraints
- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the integers in `nums` are unique.

### Example
#### Input:
`1 2 3`

#### Output:

[]
[1]
[1 2]
[1 2 3]
[1 3]
[2]
[2 3]
[3]

(Note: The order of subsets shown here is one possible valid output. Your output might have a different order, which is acceptable as long as all subsets are present and unique.)

### Concepts Covered
- Backtracking
- Recursion
- Decision Tree
- Subset Generation
- State Management in Recursive Calls