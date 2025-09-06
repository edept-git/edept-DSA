# Solutions for Subsets Unleashed: The Combination Quest

### Approach
This problem can be solved efficiently using a backtracking algorithm. The core idea behind backtracking is to build a solution incrementally, and if a path doesn't lead to a valid solution, we backtrack (undo the last choice) and try another path. For generating subsets, we can visualize this process as a decision tree.

For each element in the input array `nums`, we have two fundamental choices: either include the current element in the subset we are building, or exclude it. This binary choice for each element leads to `2^N` possible subsets for an array of `N` elements.

The algorithm proceeds as follows:
1.  Initialize an empty list to store all the final subsets (`result`).
2.  Initialize an empty list to represent the current subset being built (`current_subset`).
3.  Define a recursive helper function (often called `backtrack` or `dfs`) that takes the input array, the current starting index, the `current_subset`, and the `result` list.
4.  **Base Case**: At each step of the recursion, the `current_subset` represents a valid subset. So, add a copy of `current_subset` to the `result` list.
5.  **Recursive Step**: Iterate from the `start_index` up to the end of the input array. For each element `nums[i]`:
    a.  **Choose**: Add `nums[i]` to `current_subset`.
    b.  **Explore**: Recursively call the helper function with `i + 1` as the new `start_index` (to avoid duplicate elements and ensure distinct combinations).
    c.  **Unchoose (Backtrack)**: Remove `nums[i]` from `current_subset`. This step is crucial for exploring other paths in the decision tree and allows the `current_subset` to be reused for subsequent choices.

**Time Complexity**: There are `2^N` possible subsets for an array of size `N`. For each subset, we might perform operations like copying it to the result list, which takes O(N) time. Therefore, the total time complexity is O(N * 2^N).

**Space Complexity**: The space complexity is primarily dominated by the storage required for the `result` list. Since there are `2^N` subsets, and each subset can have up to `N` elements, the space complexity for the output is O(N * 2^N). Additionally, the recursion stack depth can go up to `N` (for the longest subset), contributing O(N) to the auxiliary space.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// A helper function to print an integer array (subset)
void printSubset(int* subset, int size) {
    printf("[");
    for (int i = 0; i < size; i++) {
        printf("%d", subset[i]);
        if (i < size - 1) {
            printf(" ");
        }
    }
    printf("]\n");
}

// Backtracking helper function to generate subsets
// For C, we'll print subsets directly to avoid complex memory management for a list of lists,
// as is common in competitive programming when the goal is to find and print all solutions.
void backtrack(int* nums, int numsSize, int* currentSubset, int currentSubsetSize, int startIdx) {
    // Base case: currentSubset is a valid subset, print it.
    printSubset(currentSubset, currentSubsetSize);

    // Recursive step: Explore choices
    for (int i = startIdx; i < numsSize; i++) {
        // Choose: Add nums[i] to currentSubset
        currentSubset[currentSubsetSize] = nums[i];

        // Explore: Recurse with the next element
        backtrack(nums, numsSize, currentSubset, currentSubsetSize + 1, i + 1);

        // Unchoose (Backtrack): Conceptually remove the last element.
        // In C with a fixed-size `currentSubset` passed by value or managing size, 
        // simply returning from the function means `currentSubsetSize` will revert for the caller.
        // No explicit `pop_back` is needed on the array itself, as we pass `currentSubsetSize + 1` 
        // to the next call, and currentSubsetSize will implicitly be its old value for the next iteration.
    }
}

// Main function to find all subsets
void findSubsets(int* nums, int numsSize) {
    // currentSubset will hold the elements for the current subset being built.
    // Max size of currentSubset is numsSize (when all elements are included).
    int* currentSubset = (int*)malloc(numsSize * sizeof(int));
    if (currentSubset == NULL) {
        fprintf(stderr, "Memory allocation failed\n");
        return;
    }

    // Start the backtracking process
    backtrack(nums, numsSize, currentSubset, 0, 0);

    free(currentSubset);
}

int main() {
    int nums[10]; // Max constraint 10 elements
    int numsSize = 0;
    int num;

    // Read input from stdin: space-separated integers on a single line
    char buffer[100]; // Buffer to read the line
    if (fgets(buffer, sizeof(buffer), stdin) == NULL) {
        // Handle error or empty input
        return 1;
    }

    char* token = strtok(buffer, " \n");
    while (token != NULL && numsSize < 10) {
        nums[numsSize++] = atoi(token);
        token = strtok(NULL, " \n");
    }
    
    // As per constraints, nums.length >= 1, so no empty array input for main logic
    // If it were allowed and empty, just [] would be the output.

    findSubsets(nums, numsSize);

    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
#include <sstream>

// Helper function for backtracking
void backtrack(const std::vector<int>& nums,
               int startIdx,
               std::vector<int>& currentSubset,
               std::vector<std::vector<int>>& result) {
    
    // Add the current subset to the result list
    result.push_back(currentSubset);

    // Explore choices
    for (int i = startIdx; i < nums.size(); ++i) {
        // Choose: Add nums[i] to currentSubset
        currentSubset.push_back(nums[i]);

        // Explore: Recurse with the next element
        backtrack(nums, i + 1, currentSubset, result);

        // Unchoose (Backtrack): Remove the last element to explore other paths
        currentSubset.pop_back();
    }
}

// Main function to find all subsets
std::vector<std::vector<int>> findSubsets(const std::vector<int>& nums) {
    std::vector<std::vector<int>> result;
    std::vector<int> currentSubset;
    backtrack(nums, 0, currentSubset, result);
    return result;
}

int main() {
    std::vector<int> nums;
    int num;
    std::string line;

    // Read a line of space-separated integers from stdin
    std::getline(std::cin, line);
    std::stringstream ss(line);
    while (ss >> num) {
        nums.push_back(num);
    }

    // Constraints say nums.length >= 1, so no empty array input for main logic
    // If it were allowed and empty, just {{}} (a list containing one empty list) would be the output.

    std::vector<std::vector<int>> result = findSubsets(nums);

    // Print the results
    for (const auto& subset : result) {
        std::cout << "[";
        for (size_t i = 0; i < subset.size(); ++i) {
            std::cout << subset[i];
            if (i < subset.size() - 1) {
                std::cout << " ";
            }
        }
        std::cout << "]\n";
    }

    return 0;
}

```

## Java Solution
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class Solution {

    // Helper function for backtracking
    private void backtrack(int[] nums,
                           int startIdx,
                           List<Integer> currentSubset,
                           List<List<Integer>> result) {

        // Add the current subset to the result list
        result.add(new ArrayList<>(currentSubset)); // Add a copy to prevent modification issues

        // Explore choices
        for (int i = startIdx; i < nums.length; i++) {
            // Choose: Add nums[i] to currentSubset
            currentSubset.add(nums[i]);

            // Explore: Recurse with the next element
            backtrack(nums, i + 1, currentSubset, result);

            // Unchoose (Backtrack): Remove the last element to explore other paths
            currentSubset.remove(currentSubset.size() - 1);
        }
    }

    // Main function to find all subsets
    public List<List<Integer>> findSubsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> currentSubset = new ArrayList<>();
        backtrack(nums, 0, currentSubset, result);
        return result;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String line = scanner.nextLine();
        scanner.close();

        // Constraints say nums.length >= 1, but handling empty input defensively.
        if (line.trim().isEmpty()) {
            System.out.println("[]"); 
            return;
        }

        String[] numStrings = line.trim().split("\\s+");
        int[] nums = new int[numStrings.length];
        for (int i = 0; i < numStrings.length; i++) {
            nums[i] = Integer.parseInt(numStrings[i]);
        }

        Solution sol = new Solution();
        List<List<Integer>> result = sol.findSubsets(nums);

        // Print the results
        for (List<Integer> subset : result) {
            System.out.print("[");
            for (int i = 0; i < subset.size(); i++) {
                System.out.print(subset.get(i));
                if (i < subset.size() - 1) {
                    System.out.print(" ");
                }
            }
            System.out.println("]");
        }
    }
}

```

## Python Solution
```python
import sys

class Solution:
    def _backtrack(self, nums, start_idx, current_subset, result):
        # Add the current subset to the result list
        result.append(list(current_subset)) # Append a copy to prevent modification issues

        # Explore choices
        for i in range(start_idx, len(nums)):
            # Choose: Add nums[i] to current_subset
            current_subset.append(nums[i])

            # Explore: Recurse with the next element
            self._backtrack(nums, i + 1, current_subset, result)

            # Unchoose (Backtrack): Remove the last element to explore other paths
            current_subset.pop()

    def find_subsets(self, nums):
        result = []
        current_subset = []
        self._backtrack(nums, 0, current_subset, result)
        return result

def main():
    line = sys.stdin.readline().strip()

    # Constraints say nums.length >= 1, but handling empty input defensively.
    if not line:
        print("[]")
        return

    nums = list(map(int, line.split()))

    sol = Solution()
    result = sol.find_subsets(nums)

    # Print the results
    for subset in result:
        print("[" + " ".join(map(str, subset)) + "]")

if __name__ == "__main__":
    main()

```

## JavaScript Solution
```javascript
const readline = require('readline');

class Solution {
    _backtrack(nums, startIdx, currentSubset, result) {
        // Add the current subset to the result list
        result.push([...currentSubset]); // Push a shallow copy to prevent modification issues

        // Explore choices
        for (let i = startIdx; i < nums.length; i++) {
            // Choose: Add nums[i] to currentSubset
            currentSubset.push(nums[i]);

            // Explore: Recurse with the next element
            this._backtrack(nums, i + 1, currentSubset, result);

            // Unchoose (Backtrack): Remove the last element to explore other paths
            currentSubset.pop();
        }
    }

    // Main function to find all subsets
    findSubsets(nums) {
        const result = [];
        const currentSubset = [];
        this._backtrack(nums, 0, currentSubset, result);
        return result;
    }
}

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    // Constraints say nums.length >= 1, but handling empty input defensively.
    if (line.trim() === '') {
        console.log("[]");
        rl.close();
        return;
    }

    const nums = line.split(' ').map(Number);

    const sol = new Solution();
    const result = sol.findSubsets(nums);

    // Print the results
    for (const subset of result) {
        console.log(`[${subset.join(' ')}]`);
    }

    rl.close();
});

```