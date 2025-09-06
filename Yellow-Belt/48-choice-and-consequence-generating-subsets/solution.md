# Solutions for Choice and Consequence: Generating Subsets

### Approach
This problem can be efficiently solved using a recursive backtracking approach. Backtracking involves exploring all possible paths (decisions) and then reverting those decisions to explore other paths. In the context of subset generation, for each element in the input array, we have two fundamental choices: either include the element in the current subset or exclude it.

The algorithm works as follows:
1.  Initialize an empty list `result` to store all generated subsets and an empty list `current_subset` to build the subset during recursion.
2.  Define a recursive helper function, say `backtrack(index, current_subset, result, nums)`.
3.  **Base Case / Decision Point:** At the beginning of each `backtrack` call, the `current_subset` represents a valid subset formed by the decisions made so far. Add a copy of this `current_subset` to the `result` list.
4.  **Recursive Step (Exploration):** Iterate from the `index` (current position) up to the end of the `nums` array.
    a.  **Choose:** Add `nums[i]` to `current_subset`.
    b.  **Explore:** Recursively call `backtrack(i + 1, current_subset, result, nums)` to consider elements from the next position onwards.
    c.  **Unchoose (Backtrack):** After the recursive call returns, remove `nums[i]` from `current_subset`. This is the crucial backtracking step, allowing the algorithm to explore paths where `nums[i]` is not included, or to revert the state for a different branch of the decision tree.

The `main` logic function initializes the `result` and `current_subset` and then calls the `backtrack` function starting from index `0`.

**Time Complexity:** The total number of subsets for a set of `N` elements is 2^N. For each subset, we perform operations like adding it to the result list, which can take O(N) time (e.g., copying elements). Therefore, the overall time complexity is O(N * 2^N).

**Space Complexity:** The space complexity is primarily determined by the storage of the `result` list and the recursion stack. The `result` list stores 2^N subsets, each with an average size of N/2 (worst case N), leading to O(N * 2^N) space. The recursion stack depth goes up to `N` (when building the largest subset), contributing O(N) auxiliary space.

## C Solution
```c
#include <stdio.n>
#include <stdlib.h>

// Dynamic array for a single subset
typedef struct {
    int* data;
    int size;
    int capacity;
} Subset;

// Dynamic array for all subsets
typedef struct {
    Subset* subsets;
    int size;
    int capacity;
} SubsetsList;

// Function to initialize a Subset
void initSubset(Subset* s) {
    s->data = NULL;
    s->size = 0;
    s->capacity = 0;
}

// Function to add an element to a Subset
void addToSubset(Subset* s, int val) {
    if (s->size == s->capacity) {
        s->capacity = (s->capacity == 0) ? 1 : s->capacity * 2;
        s->data = (int*)realloc(s->data, s->capacity * sizeof(int));
        if (s->data == NULL) {
            fprintf(stderr, "Memory allocation failed for subset data.\n");
            exit(EXIT_FAILURE);
        }
    }
    s->data[s->size++] = val;
}

// Function to remove the last element from a Subset
void removeFromSubset(Subset* s) {
    if (s->size > 0) {
        s->size--;
    }
}

// Function to initialize SubsetsList
void initSubsetsList(SubsetsList* sl) {
    sl->subsets = NULL;
    sl->size = 0;
    sl->capacity = 0;
}

// Function to add a copy of a Subset to SubsetsList
void addSubsetToList(SubsetsList* sl, const Subset* s) {
    if (sl->size == sl->capacity) {
        sl->capacity = (sl->capacity == 0) ? 1 : sl->capacity * 2;
        sl->subsets = (Subset*)realloc(sl->subsets, sl->capacity * sizeof(Subset));
        if (sl->subsets == NULL) {
            fprintf(stderr, "Memory allocation failed for subsets list.\n");
            exit(EXIT_FAILURE);
        }
    }
    
    Subset new_s;
    initSubset(&new_s);
    for (int i = 0; i < s->size; ++i) {
        addToSubset(&new_s, s->data[i]);
    }
    sl->subsets[sl->size++] = new_s;
}

// Function to free memory of a Subset
void freeSubset(Subset* s) {
    free(s->data);
    s->data = NULL;
    s->size = 0;
    s->capacity = 0;
}

// Function to free memory of SubsetsList
void freeSubsetsList(SubsetsList* sl) {
    for (int i = 0; i < sl->size; ++i) {
        freeSubset(&sl->subsets[i]);
    }
    free(sl->subsets);
    sl->subsets = NULL;
    sl->size = 0;
    sl->capacity = 0;
}

// Backtracking helper function
void backtrack(int index, int* nums, int nums_size, Subset* current_subset, SubsetsList* result_list) {
    addSubsetToList(result_list, current_subset);

    for (int i = index; i < nums_size; ++i) {
        addToSubset(current_subset, nums[i]);
        backtrack(i + 1, nums, nums_size, current_subset, result_list);
        removeFromSubset(current_subset); // Backtrack
    }
}

// Main logic function to find all subsets
SubsetsList generateSubsets(int* nums, int nums_size) {
    SubsetsList result_list;
    initSubsetsList(&result_list);

    Subset current_subset;
    initSubset(&current_subset);

    backtrack(0, nums, nums_size, &current_subset, &result_list);
    
    freeSubset(&current_subset); // Free the temp subset used in recursion
    
    return result_list;
}

int main() {
    int nums[10]; // Max 10 elements as per constraints
    int nums_size = 0;
    int val;

    // Read input numbers until newline or EOF
    // Using a loop with getchar() to correctly handle space-separated integers
    // and stop on newline, assuming single line input.
    char buffer[100]; // Small buffer for input line
    if (fgets(buffer, sizeof(buffer), stdin) != NULL) {
        char* ptr = buffer;
        while (sscanf(ptr, "%d", &val) == 1) {
            nums[nums_size++] = val;
            // Move pointer past the number and any spaces
            while (*ptr != '\0' && *ptr != ' ' && *ptr != '\n') {
                ptr++;
            }
            while (*ptr != '\0' && *ptr == ' ') {
                ptr++;
            }
            if (*ptr == '\n' || *ptr == '\0') break;
        }
    }

    SubsetsList result = generateSubsets(nums, nums_size);

    // Print the result
    for (int i = 0; i < result.size; ++i) {
        printf("[");
        for (int j = 0; j < result.subsets[i].size; ++j) {
            printf("%d", result.subsets[i].data[j]);
            if (j < result.subsets[i].size - 1) {
                printf(" ");
            }
        }
        printf("]\n");
    }

    freeSubsetsList(&result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>

void backtrack(int index, const std::vector<int>& nums, std::vector<int>& current_subset, std::vector<std::vector<int>>& result) {
    result.push_back(current_subset); // Add the current subset to the result

    for (int i = index; i < nums.size(); ++i) {
        current_subset.push_back(nums[i]); // Include nums[i]
        backtrack(i + 1, nums, current_subset, result); // Recurse with the next index
        current_subset.pop_back(); // Backtrack: remove nums[i]
    }
}

std::vector<std::vector<int>> generateSubsets(const std::vector<int>& nums) {
    std::vector<std::vector<int>> result;
    std::vector<int> current_subset;
    backtrack(0, nums, current_subset, result);
    return result;
}

int main() {
    std::string line;
    std::getline(std::cin, line);
    std::stringstream ss(line);
    
    std::vector<int> nums;
    int num;
    while (ss >> num) {
        nums.push_back(num);
    }

    std::vector<std::vector<int>> result = generateSubsets(nums);

    // Print the result
    for (const auto& subset : result) {
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
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class Solution {

    public List<List<Integer>> generateSubsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> currentSubset = new ArrayList<>();
        backtrack(0, nums, currentSubset, result);
        return result;
    }

    private void backtrack(int index, int[] nums, List<Integer> currentSubset, List<List<Integer>> result) {
        result.add(new ArrayList<>(currentSubset)); // Add a copy of the current subset

        for (int i = index; i < nums.length; i++) {
            currentSubset.add(nums[i]); // Include nums[i]
            backtrack(i + 1, nums, currentSubset, result); // Recurse with the next index
            currentSubset.remove(currentSubset.size() - 1); // Backtrack: remove nums[i]
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String line = scanner.nextLine();
        scanner.close();

        // Parse the input line into an array of integers
        String[] numStrings = line.trim().split(" ");
        
        int[] nums;
        if (line.trim().isEmpty()) { // Handle empty input case
            nums = new int[0];
        } else {
            nums = new int[numStrings.length];
            for (int i = 0; i < numStrings.length; i++) {
                nums[i] = Integer.parseInt(numStrings[i]);
            }
        }

        Solution sol = new Solution();
        List<List<Integer>> result = sol.generateSubsets(nums);

        // Print the result
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
    def subsets(self, nums: list[int]) -> list[list[int]]:
        result = []
        current_subset = []
        
        def backtrack(index):
            result.append(list(current_subset)) # Add a copy of the current subset
            
            for i in range(index, len(nums)):
                current_subset.append(nums[i]) # Include nums[i]
                backtrack(i + 1) # Recurse with the next index
                current_subset.pop() # Backtrack: remove nums[i]
        
        backtrack(0)
        return result

def main():
    line = sys.stdin.readline().strip()
    
    if line:
        nums = list(map(int, line.split()))
    else:
        nums = []

    sol = Solution()
    result = sol.subsets(nums)

    # Print the result
    for subset in result:
        sys.stdout.write("[")
        sys.stdout.write(" ".join(map(str, subset)))
        sys.stdout.write("]\n")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
class Solution {
    subsets(nums) {
        const result = [];
        const currentSubset = [];

        function backtrack(index) {
            result.push([...currentSubset]); // Add a copy of the current subset

            for (let i = index; i < nums.length; i++) {
                currentSubset.push(nums[i]); // Include nums[i]
                backtrack(i + 1); // Recurse with the next index
                currentSubset.pop(); // Backtrack: remove nums[i]
            }
        }

        backtrack(0);
        return result;
    }
}

// Function to handle input and output for the platform
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    rl.on('line', (line) => {
        let nums;
        if (line.trim() === "") {
            nums = [];
        } else {
            nums = line.split(' ').map(Number);
        }

        const sol = new Solution();
        const result = sol.subsets(nums);

        // Print the result
        for (const subset of result) {
            process.stdout.write("[");
            process.stdout.write(subset.join(" "));
            process.stdout.write("]\n");
        }
        rl.close(); // Close the readline interface after processing input
    });
}

// Ensure main is called if script is executed directly
if (require.main === module) {
    main();
}
```