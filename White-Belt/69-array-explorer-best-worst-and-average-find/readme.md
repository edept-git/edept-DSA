### Description
You are given an array of integers and a target integer. Your task is to implement a linear search algorithm to find the target in the array. In addition to returning the index of the target (or -1 if not found), you must also count the total number of comparisons made during the search.

This problem helps you understand the concepts of Best, Worst, and Average case time complexity by observing how the number of comparisons changes based on the target's position.

### Constraints
- The array `nums` will have a length `N` between 1 and 100.
- Each element `nums[i]` will be an integer between -100 and 100.
- The target integer `target` will be between -100 and 100.

### Example
**Input:**
N = 5
nums = [10, 20, 30, 40, 50]
target = 30

**Output:**
Found at index 2 in 3 comparisons

**Input:**
N = 4
nums = [5, 15, 25, 35]
target = 40

**Output:**
Not found in 4 comparisons

### Concepts Covered
- Linear Search Algorithm
- Time Complexity Analysis
- Best Case Scenario (O(1))
- Worst Case Scenario (O(N))
- Average Case Scenario (O(N))