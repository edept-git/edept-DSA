# Solutions for The K-Combination Conundrum

### Approach
This problem is a classic application of the backtracking algorithm. Backtracking is a general algorithmic technique for finding all (or some) solutions to computational problems, typically by trying to build a solution incrementally, and abandoning a partial solution ("backtracking") as soon as it determines that the partial solution cannot be completed to a valid solution.

For this problem, we can define a recursive helper function, let's call it `backtrack(start_num, current_combination)`:
1.  **Base Case**: If the `current_combination` already contains `k` elements, it means we have found a valid combination. We add a copy of this `current_combination` to our list of results and then return.
2.  **Pruning (Optimization)**: Before starting the loop in the recursive step, we can check if it's even possible to form a combination of size `k` with the remaining numbers. If `(k - current_combination.size()) > (n - start_num + 1)`, it means we need more elements than are available from `start_num` to `n`. In this case, we can immediately return, avoiding unnecessary exploration.
3.  **Recursive Step**: We iterate through numbers from `start_num` up to `n`. For each number `i` in this range:
    *   We "make a choice" by adding `i` to our `current_combination`.
    *   We then recursively call `backtrack(i + 1, current_combination)`. We pass `i + 1` as the new `start_num` to ensure that we only pick numbers greater than the current one, preventing duplicate combinations (like `[2,1]` if `[1,2]` is already valid) and ensuring elements within a combination are distinct and in ascending order.
    *   After the recursive call returns, we "undo the choice" by removing `i` from `current_combination`. This crucial "backtracking" step allows us to explore other possibilities.

This process systematically explores all possible paths in the decision tree, adding valid combinations to our result list.

**Data Structures**:
*   A list (or vector/array) to store the `current_combination` being built.
*   A list of lists (or vector of vectors/array of arrays) to store all the valid combinations found.

**Time Complexity**: The number of unique combinations of `k` elements chosen from `n` is given by the binomial coefficient "n choose k" or `C(n, k) = n! / (k! * (n-k)!)`. For each combination found, we perform operations proportional to `k` (e.g., copying the combination to the result list). Thus, the overall time complexity is approximately `O(C(n, k) * k)`. In the worst case (e.g., `k = n/2`), `C(n, k)` can be very large, close to `O(2^n)`. Given `n <= 15`, this is manageable.

**Space Complexity**: The space complexity is primarily determined by the storage required for the result list and the recursion stack. The result list stores `C(n, k)` combinations, each of size `k`, leading to `O(C(n, k) * k)` space. The maximum depth of the recursion stack is `k`, as we add one element at a time until the combination is full, resulting in `O(k)` space for the stack. Therefore, the total space complexity is `O(C(n, k) * k)`.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Helper function for backtracking
void backtrack(int n, int k, int start, int* current_combination, int current_size,
               int*** results, int* result_count, int** result_col_sizes) {
    // Base case: if current_combination has k elements, add it to results
    if (current_size == k) {
        // Allocate space for the new combination
        (*results) = (int**)realloc(*results, (*result_count + 1) * sizeof(int*));
        if (*results == NULL) {
            perror("Failed to reallocate results");
            exit(EXIT_FAILURE);
        }
        (*results)[*result_count] = (int*)malloc(k * sizeof(int));
        if ((*results)[*result_count] == NULL) {
            perror("Failed to allocate combination");
            exit(EXIT_FAILURE);
        }

        // Copy current_combination to results
        for (int i = 0; i < k; i++) {
            (*results)[*result_count][i] = current_combination[i];
        }

        // Store column size
        (*result_col_sizes) = (int*)realloc(*result_col_sizes, (*result_count + 1) * sizeof(int));
        if (*result_col_sizes == NULL) {
            perror("Failed to reallocate column sizes");
            exit(EXIT_FAILURE);
        }
        (*result_col_sizes)[*result_count] = k;

        (*result_count)++;
        return;
    }

    // Optimization: if remaining elements are not enough to form a combination
    // (n - start + 1) is the count of numbers from 'start' to 'n'
    // (k - current_size) is the number of elements we still need
    if (k - current_size > n - start + 1) {
        return;
    }

    // Recursive step: iterate from start to n
    for (int i = start; i <= n; i++) {
        // Make a choice: add i to current_combination
        current_combination[current_size] = i;

        // Recurse: explore combinations starting from i + 1
        backtrack(n, k, i + 1, current_combination, current_size + 1,
                  results, result_count, result_col_sizes);
        
        // No explicit "undo" needed for simple values in C arrays when working with indices
        // The next iteration or a return will overwrite/ignore this index
    }
}

// Main function to find combinations
int** combine(int n, int k, int* returnSize, int** returnColumnSizes) {
    if (k <= 0 || k > n) {
        *returnSize = 0;
        *returnColumnSizes = NULL;
        return NULL;
    }

    int** results = NULL;
    *returnSize = 0;
    *returnColumnSizes = NULL;

    // current_combination acts as a temporary buffer for elements.
    // Max k is 15, so a small fixed-size array is safe for the stack.
    // If k could be very large, this would need to be dynamic.
    int* current_combination = (int*)malloc(k * sizeof(int));
    if (current_combination == NULL) {
        perror("Failed to allocate current_combination buffer");
        exit(EXIT_FAILURE);
    }

    backtrack(n, k, 1, current_combination, 0, &results, returnSize, returnColumnSizes);

    free(current_combination); // Free the temporary buffer
    return results;
}

// Helper to print results for main
void printCombinations(int** combinations, int numRows, int* colSizes) {
    printf("[\n");
    for (int i = 0; i < numRows; i++) {
        printf("  [");
        for (int j = 0; j < colSizes[i]; j++) {
            printf("%d%s", combinations[i][j], (j == colSizes[i] - 1) ? "" : ",");
        }
        printf("]%s\n", (i == numRows - 1) ? "" : ",");
    }
    printf("]\n");
}

int main() {
    int n, k;
    if (scanf("%d %d", &n, &k) != 2) {
        fprintf(stderr, "Failed to read n and k\n");
        return 1;
    }

    int returnSize;
    int* returnColumnSizes;
    int** result = combine(n, k, &returnSize, &returnColumnSizes);

    printCombinations(result, returnSize, returnColumnSizes);

    // Free allocated memory
    for (int i = 0; i < returnSize; i++) {
        free(result[i]);
    }
    free(result);
    free(returnColumnSizes);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> 

class Solution {
private:
    std::vector<std::vector<int>> allCombinations;
    std::vector<int> currentCombination;

    void backtrack(int n, int k, int start_num) {
        // Base case: if currentCombination has k elements, add it to results
        if (currentCombination.size() == k) {
            allCombinations.push_back(currentCombination);
            return;
        }

        // Optimization: if remaining elements are not enough to form a combination
        // (n - start_num + 1) is the count of numbers from 'start_num' to 'n'
        // (k - currentCombination.size()) is the number of elements we still need
        if (k - currentCombination.size() > n - start_num + 1) {
            return;
        }

        // Recursive step: iterate from start_num to n
        for (int i = start_num; i <= n; ++i) {
            // Make a choice: add i to currentCombination
            currentCombination.push_back(i);

            // Recurse: explore combinations starting from i + 1
            backtrack(n, k, i + 1);

            // Undo the choice (backtrack): remove i from currentCombination
            currentCombination.pop_back();
        }
    }

public:
    std::vector<std::vector<int>> combine(int n, int k) {
        allCombinations.clear(); 
        currentCombination.clear(); 

        if (k <= 0 || k > n) {
            return allCombinations; 
        }

        backtrack(n, k, 1);
        return allCombinations;
    }
};

void printCombinations(const std::vector<std::vector<int>>& combinations) {
    std::cout << "[\n";
    for (size_t i = 0; i < combinations.size(); ++i) {
        std::cout << "  [";
        for (size_t j = 0; j < combinations[i].size(); ++j) {
            std::cout << combinations[i][j] << (j == combinations[i].size() - 1 ? "" : ",");
        }
        std::cout << "]" << (i == combinations.size() - 1 ? "" : ",") << "\n";
    }
    std::cout << "]\n";
}

int main() {
    int n, k;
    if (!(std::cin >> n >> k)) {
        std::cerr << "Failed to read n and k\n";
        return 1;
    }

    Solution sol;
    std::vector<std::vector<int>> result = sol.combine(n, k);

    printCombinations(result);

    return 0;
}
```

## Java Solution
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Solution {
    List<List<Integer>> allCombinations;
    List<Integer> currentCombination;

    private void backtrack(int n, int k, int startNum) {
        // Base case: if currentCombination has k elements, add it to results
        if (currentCombination.size() == k) {
            allCombinations.add(new ArrayList<>(currentCombination)); // Add a copy
            return;
        }

        // Optimization: if remaining elements are not enough to form a combination
        // (n - startNum + 1) is the count of numbers from 'startNum' to 'n'
        // (k - currentCombination.size()) is the number of elements we still need
        if (k - currentCombination.size() > n - startNum + 1) {
            return;
        }

        // Recursive step: iterate from startNum to n
        for (int i = startNum; i <= n; i++) {
            // Make a choice: add i to currentCombination
            currentCombination.add(i);

            // Recurse: explore combinations starting from i + 1
            backtrack(n, k, i + 1);

            // Undo the choice (backtrack): remove i from currentCombination
            currentCombination.remove(currentCombination.size() - 1);
        }
    }

    public List<List<Integer>> combine(int n, int k) {
        allCombinations = new ArrayList<>();
        currentCombination = new ArrayList<>();

        if (k <= 0 || k > n) {
            return allCombinations; // Return empty list
        }

        backtrack(n, k, 1);
        return allCombinations;
    }
}

public class Main {
    public static void printCombinations(List<List<Integer>> combinations) {
        System.out.println("[");
        for (int i = 0; i < combinations.size(); i++) {
            System.out.print("  [");
            List<Integer> combination = combinations.get(i);
            for (int j = 0; j < combination.size(); j++) {
                System.out.print(combination.get(j));
                if (j < combination.size() - 1) {
                    System.out.print(",");
                }
            }
            System.out.print("]");
            if (i < combinations.size() - 1) {
                System.out.print(",");
            }
            System.out.println();
        }
        System.out.println("]");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int k = scanner.nextInt();
        scanner.close();

        Solution sol = new Solution();
        List<List<Integer>> result = sol.combine(n, k);

        printCombinations(result);
    }
}
```

## Python Solution
```python
import sys

class Solution:
    def combine(self, n: int, k: int) -> list[list[int]]:
        all_combinations = []
        current_combination = []

        if k <= 0 or k > n:
            return all_combinations

        def backtrack(start_num: int):
            # Base case: if current_combination has k elements, add it to results
            if len(current_combination) == k:
                all_combinations.append(list(current_combination)) # Add a copy
                return

            # Optimization: if remaining elements are not enough to form a combination
            # (n - start_num + 1) is the count of numbers from 'start_num' to 'n'
            # (k - len(current_combination)) is the number of elements we still need
            if k - len(current_combination) > n - start_num + 1:
                return

            # Recursive step: iterate from start_num to n
            for i in range(start_num, n + 1):
                # Make a choice: add i to current_combination
                current_combination.append(i)

                # Recurse: explore combinations starting from i + 1
                backtrack(i + 1)

                # Undo the choice (backtrack): remove i from current_combination
                current_combination.pop()
        
        backtrack(1)
        return all_combinations

def print_combinations(combinations: list[list[int]]):
    sys.stdout.write("[")
    if len(combinations) > 0:
        sys.stdout.write("\n")
    for i, combination in enumerate(combinations):
        sys.stdout.write("  [")
        sys.stdout.write(",".join(map(str, combination)))
        sys.stdout.write("]")
        if i < len(combinations) - 1:
            sys.stdout.write(",")
        sys.stdout.write("\n")
    sys.stdout.write("]\n")

if __name__ == '__main__':
    lines = sys.stdin.readlines()
    n, k = map(int, lines[0].strip().split())

    sol = Solution()
    result = sol.combine(n, k)

    print_combinations(result)

```

## JavaScript Solution
```javascript
const readline = require('readline');

// The Solution class structure
class Solution {
    constructor() {
        this.allCombinations = [];
        this.currentCombination = [];
    }

    backtrack(n, k, startNum) {
        // Base case: if currentCombination has k elements, add it to results
        if (this.currentCombination.length === k) {
            this.allCombinations.push([...this.currentCombination]); // Add a copy
            return;
        }

        // Optimization: if remaining elements are not enough to form a combination
        // (n - startNum + 1) is the count of numbers from 'startNum' to 'n'
        // (k - this.currentCombination.length) is the number of elements we still need
        if (k - this.currentCombination.length > n - startNum + 1) {
            return;
        }

        // Recursive step: iterate from startNum to n
        for (let i = startNum; i <= n; i++) {
            // Make a choice: add i to currentCombination
            this.currentCombination.push(i);

            // Recurse: explore combinations starting from i + 1
            this.backtrack(n, k, i + 1);

            // Undo the choice (backtrack): remove i from currentCombination
            this.currentCombination.pop();
        }
    }

    combine(n, k) {
        this.allCombinations = []; // Clear for new calls
        this.currentCombination = []; // Clear for new calls

        if (k <= 0 || k > n) {
            return this.allCombinations; // Return empty array
        }

        this.backtrack(n, k, 1);
        return this.allCombinations;
    }
}

// Function to print combinations in the specified format
function printCombinations(combinations) {
    let output = "[";
    if (combinations.length > 0) {
        output += "\n";
    }
    for (let i = 0; i < combinations.length; i++) {
        output += "  [";
        output += combinations[i].join(",");
        output += "]";
        if (i < combinations.length - 1) {
            output += ",";
        }
        output += "\n";
    }
    output += "]\n";
    console.log(output);
}

// Main execution block to handle input and output
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];

rl.on('line', (line) => {
    inputLines.push(line);
}).on('close', () => {
    const [n, k] = inputLines[0].split(' ').map(Number);

    const sol = new Solution();
    const result = sol.combine(n, k);

    printCombinations(result);
});

```