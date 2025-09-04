# Solutions for Branching Out: All Subsets

### Approach
This problem can be effectively solved using a backtracking algorithm, which is a specialized form of recursion. The core idea is to explore all possible choices at each step and then "backtrack" (undo the choice) to explore other alternatives.

For generating all subsets, we can define a recursive helper function, let's call it `generateSubsets(index, currentSubset)`.
1.  **Base Case:** At each recursive call, the first step is to add a *copy* of the `currentSubset` to our `result` list. This is because `currentSubset` represents a valid subset at that point in the recursion.
2.  **Recursive Step (Explore Choices):** We then iterate through the remaining elements in the input array `nums`, starting from the `index`. For each element `nums[i]`:
    *   **Include:** Add `nums[i]` to `currentSubset`.
    *   **Recurse:** Make a recursive call to `generateSubsets(i + 1, currentSubset)` to explore further subsets starting from the next element. This ensures that elements are added in increasing order of their original index, preventing duplicate subsets (like `[1, 2]` and `[2, 1]`) and ensuring combinations are generated.
    *   **Backtrack:** After the recursive call returns, remove `nums[i]` from `currentSubset`. This step is crucial for backtracking; it undoes the "include" choice, allowing `currentSubset` to be in the correct state for the next iteration of the loop (to explore subsets that do *not* include `nums[i]` at this level, or to prepare for the next element `nums[i+1]`).

**Data Structures:**
-   A temporary list (e.g., `ArrayList` in Java, `vector` in C++, `list` in Python) to build the `currentSubset` during recursion.
-   A main list (e.g., `List<List<Integer>>` in Java) to store all the generated subsets.

**Time Complexity:**
The algorithm explores all possible subsets. For an array of `N` elements, there are `2^N` possible subsets. For each subset, we perform operations like adding elements to a temporary list and copying the temporary list to the result list. In the worst case, adding an element to `currentSubset` and then copying `currentSubset` to `result` can take O(N) time (for a subset of size N). Thus, the total time complexity is O(N * 2^N).

**Space Complexity:**
The space complexity is also O(N * 2^N). This is primarily due to storing all `2^N` subsets in the `result` list, where each subset can contain up to `N` elements. Additionally, the recursion stack depth can go up to O(N) in the worst case.


## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // For malloc, free, atoi
#include <string.h> // For strtok

// Global variables for the current subset and its size for simpler C management.
// This is a common simplification for Yellow Belt C problems with recursion
// that would otherwise require complex dynamic array management.
// For a production system, these would typically be passed as parameters or use a struct.
int currentSubset_c[10]; // Max subset size based on constraints
int currentSubsetSize_c = 0;

// Helper function to print a subset
void printSubset_c(int* subset, int size) {
    printf("[");
    for (int i = 0; i < size; i++) {
        printf("%d", subset[i]);
        if (i < size - 1) {
            printf(" ");
        }
    }
    printf("]\n");
}

// Core logic: Backtracking function to generate and print all subsets
void generateSubsetsRecursive_c(int* nums, int numsSize, int startIndex) {
    // Base Case: Add the current subset to the result (print it)
    printSubset_c(currentSubset_c, currentSubsetSize_c);

    // Recursive Step: Explore choices
    for (int i = startIndex; i < numsSize; i++) {
        // Include nums[i]
        currentSubset_c[currentSubsetSize_c++] = nums[i];

        // Recurse with the next element
        generateSubsetsRecursive_c(nums, numsSize, i + 1);

        // Backtrack: Remove nums[i]
        currentSubsetSize_c--;
    }
}

// Main function to initiate the process
void findAllSubsets_c(int* nums, int numsSize) {
    currentSubsetSize_c = 0; // Reset for each call to findAllSubsets
    generateSubsetsRecursive_c(nums, numsSize, 0);
}

int main() {
    int nums[10]; // Max 10 elements based on constraints
    int count = 0;
    char line[100]; // Buffer to read a line, max length for 10 elements and spaces/signs

    // Read input line (space-separated integers) from stdin
    if (fgets(line, sizeof(line), stdin) != NULL) {
        // Remove trailing newline character if present
        line[strcspn(line, "\n")] = 0;

        // Tokenize the string to extract numbers
        char *token = strtok(line, " ");
        while (token != NULL && count < 10) {
            nums[count++] = atoi(token);
            token = strtok(NULL, " ");
        }
    }

    findAllSubsets_c(nums, count);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <algorithm> // Not strictly needed, but common for array operations

// Core logic: Backtracking function to generate all subsets
void generateSubsetsRecursive(std::vector<std::vector<int>>& result,
                               std::vector<int>& currentSubset,
                               const std::vector<int>& nums,
                               int startIndex) {
    // Base Case: Add a copy of the current subset to the result
    result.push_back(currentSubset);

    // Recursive Step: Explore choices
    for (int i = startIndex; i < nums.size(); ++i) {
        // Include nums[i]
        currentSubset.push_back(nums[i]);

        // Recurse with the next element
        generateSubsetsRecursive(result, currentSubset, nums, i + 1);

        // Backtrack: Remove nums[i]
        currentSubset.pop_back();
    }
}

// Main function to initiate the process and return all subsets
std::vector<std::vector<int>> findAllSubsets(const std::vector<int>& nums) {
    std::vector<std::vector<int>> result;
    std::vector<int> currentSubset;
    generateSubsetsRecursive(result, currentSubset, nums, 0);
    return result;
}

int main() {
    std::vector<int> nums;
    std::string line;
    
    // Read the entire line from stdin
    std::getline(std::cin, line);
    
    // Use stringstream to parse space-separated integers
    std::stringstream ss(line);
    int number;
    while (ss >> number) {
        nums.push_back(number);
    }

    std::vector<std::vector<int>> subsets = findAllSubsets(nums);

    // Print the results
    for (const auto& subset : subsets) {
        std::cout << "[";
        for (size_t i = 0; i < subset.size(); ++i) {
            std::cout << subset[i];
            if (i < subset.size() - 1) {
                std::cout << " ";
            }
        }
        std::cout << "]" << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
// import java.util.Arrays; // Not strictly needed, but common for array operations

public class Solution {

    // Core logic: Backtracking function to generate all subsets
    private void generateSubsetsRecursive(List<List<Integer>> result,
                                          List<Integer> currentSubset,
                                          int[] nums,
                                          int startIndex) {
        // Base Case: Add a copy of the current subset to the result
        result.add(new ArrayList<>(currentSubset));

        // Recursive Step: Explore choices
        for (int i = startIndex; i < nums.length; i++) {
            // Include nums[i]
            currentSubset.add(nums[i]);

            // Recurse with the next element
            generateSubsetsRecursive(result, currentSubset, nums, i + 1);

            // Backtrack: Remove nums[i]
            currentSubset.remove(currentSubset.size() - 1);
        }
    }

    // Main function to initiate the process and return all subsets
    public List<List<Integer>> findAllSubsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> currentSubset = new ArrayList<>();
        generateSubsetsRecursive(result, currentSubset, nums, 0);
        return result;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String line = scanner.nextLine();
        scanner.close();

        // Parse input string into an array of integers
        int[] nums;
        if (line.trim().isEmpty()) {
            nums = new int[0];
        } else {
            String[] numStrings = line.trim().split(" ");
            nums = new int[numStrings.length];
            for (int i = 0; i < numStrings.length; i++) {
                nums[i] = Integer.parseInt(numStrings[i]);
            }
        }

        Solution sol = new Solution();
        List<List<Integer>> subsets = sol.findAllSubsets(nums);

        // Print the results
        for (List<Integer> subset : subsets) {
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
    def _generate_subsets_recursive(self, result, current_subset, nums, start_index):
        # Base Case: Add a copy of the current subset to the result
        result.append(list(current_subset))

        # Recursive Step: Explore choices
        for i in range(start_index, len(nums)):
            # Include nums[i]
            current_subset.append(nums[i])

            # Recurse with the next element
            self._generate_subsets_recursive(result, current_subset, nums, i + 1)

            # Backtrack: Remove nums[i]
            current_subset.pop()

    def find_all_subsets(self, nums):
        result = []
        current_subset = []
        self._generate_subsets_recursive(result, current_subset, nums, 0)
        return result

def main():
    line = sys.stdin.readline().strip()
    
    nums = []
    if line: # Handle empty line for an empty array
        nums = list(map(int, line.split()))

    sol = Solution()
    subsets = sol.find_all_subsets(nums)

    # Print the results
    for subset in subsets:
        print("[", end="")
        print(*subset, sep=" ", end="") # Pythonic way to print list elements space-separated
        print("]")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

// Core logic: Backtracking function to generate all subsets
function generateSubsetsRecursive(result, currentSubset, nums, startIndex) {
    // Base Case: Add a copy of the current subset to the result
    result.push([...currentSubset]); // Use spread operator for shallow copy

    // Recursive Step: Explore choices
    for (let i = startIndex; i < nums.length; i++) {
        // Include nums[i]
        currentSubset.push(nums[i]);

        // Recurse with the next element
        generateSubsetsRecursive(result, currentSubset, nums, i + 1);

        // Backtrack: Remove nums[i]
        currentSubset.pop();
    }
}

// Main function to initiate the process and return all subsets
function findAllSubsets(nums) {
    const result = [];
    const currentSubset = [];
    generateSubsetsRecursive(result, currentSubset, nums, 0);
    return result;
}

// Set up readline interface for input
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    let nums = [];
    if (line.trim() !== "") {
        nums = line.split(' ').map(Number);
    }

    const subsets = findAllSubsets(nums);

    // Print the results
    for (const subset of subsets) {
        console.log(`[${subset.join(' ')}]`);
    }

    rl.close();
});
```