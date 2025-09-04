# Solutions for Orderly Explorations: Permutation Paths

### Approach
This problem is a classic example of backtracking. The core idea is to build a solution incrementally, and if a path doesn't lead to a valid solution, we backtrack (undo our last choice) and try another path.

**Algorithm:**
1.  **Define a recursive backtracking function:** This function will take the original `nums` array, a `current_permutation` (which stores the permutation being built), and a `visited` array (or a similar mechanism to track used elements).
2.  **Base Case:** If the `current_permutation` has the same number of elements as `nums`, it means we have formed a complete permutation. Add this `current_permutation` to our list of `results`.
3.  **Recursive Step:** Iterate through each number in the original `nums` array.
    *   For each number, check if it has already been used in the `current_permutation` (using the `visited` array).
    *   If the number has *not* been used:
        *   **Choose:** Add the number to `current_permutation` and mark it as `visited`.
        *   **Explore:** Recursively call the backtracking function.
        *   **Unchoose (Backtrack):** Remove the number from `current_permutation` and unmark it as `visited`. This step is crucial; it allows us to explore other paths by undoing the previous choice.

**Data Structures:**
*   `nums`: The input array.
*   `current_permutation`: A list/array to store the permutation being constructed at each step of the recursion.
*   `visited`: A boolean array or a set to keep track of which elements from `nums` have already been included in `current_permutation` to avoid duplicates within a single permutation.
*   `results`: A list of lists/arrays to store all the valid permutations found.

**Time Complexity:**
The time complexity is `O(N * N!)`, where `N` is the number of elements in `nums`. There are `N!` possible permutations. For each permutation, we perform `N` operations (to copy it or add its elements to the `results` list). The recursive calls also involve `N` choices at each level, and the depth of recursion is `N`.

**Space Complexity:**
The space complexity is `O(N)` for the recursion stack and the `current_permutation` array/list, as well as the `visited` array. If we consider the space required to store the `results`, it would be `O(N * N!)` as there are `N!` permutations, each of length `N`. However, typically, auxiliary space complexity excludes the output storage.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// Helper function to print a single permutation in the format [x,y,z]
void printPermutation(int* arr, int size) {
    printf("[");
    for (int i = 0; i < size; i++) {
        printf("%d", arr[i]);
        if (i < size - 1) {
            printf(",");
        }
    }
    printf("]");
}

// Recursive backtracking function
// count_ptr is used to correctly format the output with commas between permutations
void backtrack(int* nums, int numsSize, int* currentPermutation, bool* visited, int k, int* count_ptr) {
    // Base case: if k equals numsSize, a complete permutation is formed
    if (k == numsSize) {
        if (*count_ptr > 0) {
            printf(",");
        }
        printPermutation(currentPermutation, numsSize);
        (*count_ptr)++;
        return;
    }

    // Recursive step: iterate through nums
    for (int i = 0; i < numsSize; i++) {
        if (!visited[i]) {
            // Choose: add nums[i] to currentPermutation
            currentPermutation[k] = nums[i];
            visited[i] = true;

            // Explore: recursively call for next element
            backtrack(nums, numsSize, currentPermutation, visited, k + 1, count_ptr);

            // Unchoose (Backtrack): remove nums[i] from currentPermutation and mark as unvisited
            visited[i] = false;
        }
    }
}

// Main logic function to initiate finding permutations
void solvePermutations(int* nums, int numsSize) {
    if (numsSize == 0) {
        printf("[]\n");
        return;
    }

    int* currentPermutation = (int*)malloc(sizeof(int) * numsSize);
    bool* visited = (bool*)calloc(numsSize, sizeof(bool)); // calloc initializes to false
    int permutationCount = 0; // Counter for correct comma separation

    printf("["); // Start outer list
    backtrack(nums, numsSize, currentPermutation, visited, 0, &permutationCount);
    printf("]\n"); // End outer list

    free(currentPermutation);
    free(visited);
}

int main() {
    int n;
    scanf("%d", &n);

    int* nums = NULL;
    if (n > 0) {
        nums = (int*)malloc(sizeof(int) * n);
        for (int i = 0; i < n; i++) {
            scanf("%d", &nums[i]);
        }
    }
    
    solvePermutations(nums, n); // Call the main logic function

    if (nums != NULL) {
        free(nums);
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> 

// Helper function for backtracking
void backtrack(std::vector<int>& nums, std::vector<int>& currentPermutation, 
               std::vector<bool>& visited, std::vector<std::vector<int>>& results) {
    // Base case: if currentPermutation is complete
    if (currentPermutation.size() == nums.size()) {
        results.push_back(currentPermutation); // Add a copy
        return;
    }

    // Recursive step: iterate through nums
    for (int i = 0; i < nums.size(); ++i) {
        if (!visited[i]) {
            // Choose
            currentPermutation.push_back(nums[i]);
            visited[i] = true;

            // Explore
            backtrack(nums, currentPermutation, visited, results);

            // Unchoose (Backtrack)
            visited[i] = false;
            currentPermutation.pop_back();
        }
    }
}

// Main logic function
std::vector<std::vector<int>> permute(std::vector<int>& nums) {
    std::vector<std::vector<int>> results;
    if (nums.empty()) {
        return results;
    }

    std::vector<int> currentPermutation;
    std::vector<bool> visited(nums.size(), false); // Initialize all to false

    backtrack(nums, currentPermutation, visited, results);
    return results;
}

// Helper function to print the vector of vectors in the required format
void printResults(const std::vector<std::vector<int>>& results) {
    std::cout << "[";
    for (size_t i = 0; i < results.size(); ++i) {
        std::cout << "[";
        for (size_t j = 0; j < results[i].size(); ++j) {
            std::cout << results[i][j];
            if (j < results[i].size() - 1) {
                std::cout << ",";
            }
        }
        std::cout << "]";
        if (i < results.size() - 1) {
            std::cout << ",";
        }
    }
    std::cout << "]" << std::endl;
}

int main() {
    int n;
    std::cin >> n;

    std::vector<int> nums(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> nums[i];
    }

    // Call the main logic function
    std::vector<std::vector<int>> allPermutations = permute(nums);

    // Print the results
    printResults(allPermutations);

    return 0;
}
```

## Java Solution
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Solution {

    // Helper function for backtracking
    private void backtrack(int[] nums, List<Integer> currentPermutation, 
                           boolean[] visited, List<List<Integer>> results) {
        // Base case: if currentPermutation is complete
        if (currentPermutation.size() == nums.length) {
            results.add(new ArrayList<>(currentPermutation)); // Add a copy
            return;
        }

        // Recursive step: iterate through nums
        for (int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                // Choose
                currentPermutation.add(nums[i]);
                visited[i] = true;

                // Explore
                backtrack(nums, currentPermutation, visited, results);

                // Unchoose (Backtrack)
                visited[i] = false;
                currentPermutation.remove(currentPermutation.size() - 1);
            }
        }
    }

    // Main logic function
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            return results;
        }

        List<Integer> currentPermutation = new ArrayList<>();
        boolean[] visited = new boolean[nums.length]; // All initialized to false

        backtrack(nums, currentPermutation, visited, results);
        return results;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }
        scanner.close();

        Solution sol = new Solution();
        List<List<Integer>> allPermutations = sol.permute(nums);

        // Print the results in the required format
        System.out.print("[");
        for (int i = 0; i < allPermutations.size(); i++) {
            List<Integer> perm = allPermutations.get(i);
            System.out.print("[");
            for (int j = 0; j < perm.size(); j++) {
                System.out.print(perm.get(j));
                if (j < perm.size() - 1) {
                    System.out.print(",");
                }
            }
            System.out.print("]");
            if (i < allPermutations.size() - 1) {
                System.out.print(",");
            }
        }
        System.out.println("]");
    }
}
```

## Python Solution
```python
import json

class Solution:
    def _backtrack(self, nums, current_permutation, visited, results):
        # Base case: if current_permutation is complete
        if len(current_permutation) == len(nums):
            results.append(list(current_permutation)) # Add a copy
            return

        # Recursive step: iterate through nums
        for i in range(len(nums)):
            if not visited[i]:
                # Choose
                current_permutation.append(nums[i])
                visited[i] = True

                # Explore
                self._backtrack(nums, current_permutation, visited, results)

                # Unchoose (Backtrack)
                visited[i] = False
                current_permutation.pop()

    def permute(self, nums):
        results = []
        if not nums:
            return results

        current_permutation = []
        visited = [False] * len(nums) # Initialize all to False

        self._backtrack(nums, current_permutation, visited, results)
        return results

def main():
    n = int(input())
    # Read space-separated integers
    nums = list(map(int, input().split()))

    sol = Solution()
    all_permutations = sol.permute(nums)

    # Print the results in the required JSON-like format, no spaces.
    print(json.dumps(all_permutations).replace(" ", ""))

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

class Solution {
    _backtrack(nums, currentPermutation, visited, results) {
        // Base case: if currentPermutation is complete
        if (currentPermutation.length === nums.length) {
            results.push([...currentPermutation]); // Add a copy
            return;
        }

        // Recursive step: iterate through nums
        for (let i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                // Choose
                currentPermutation.push(nums[i]);
                visited[i] = true;

                // Explore
                this._backtrack(nums, currentPermutation, visited, results);

                // Unchoose (Backtrack)
                visited[i] = false;
                currentPermutation.pop();
            }
        }
    }

    permute(nums) {
        const results = [];
        if (!nums || nums.length === 0) {
            return results;
        }

        const currentPermutation = [];
        const visited = new Array(nums.length).fill(false); // Initialize all to false

        this._backtrack(nums, currentPermutation, visited, results);
        return results;
    }
}

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(line);
}).on('close', () => {
    const n = parseInt(inputLines[0]);
    const nums = inputLines[1].split(' ').map(Number);

    const sol = new Solution();
    const allPermutations = sol.permute(nums);

    // Print the results in the required JSON-like format, no spaces.
    console.log(JSON.stringify(allPermutations).replace(/\s/g, ''));
});
```