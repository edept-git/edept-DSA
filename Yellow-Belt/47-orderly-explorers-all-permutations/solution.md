# Solutions for Orderly Explorers: All Permutations

### Approach
This problem can be efficiently solved using a backtracking algorithm. The core idea is to explore all possible choices at each step and then undo those choices (backtrack) to explore other possibilities.

We can define a recursive helper function that takes the current state of the permutation being built, the original string (or character array), and a way to keep track of which characters have already been used.

1.  **Base Case:** If the length of the current permutation being built equals the length of the original string, it means we have formed a complete permutation. We print this permutation and return.

2.  **Recursive Step:** Iterate through each character of the original string.
    *   For each character, check if it has already been used in the current permutation. This can be done using a boolean array (or hash set) `visited` of the same size as the string, initialized to `false`.
    *   If the character has not been used:
        *   **Choose:** Mark the character as used, and append it to our current permutation.
        *   **Explore:** Recursively call the helper function to build the next part of the permutation.
        *   **Unchoose (Backtrack):** After the recursive call returns, unmark the character as used, and remove it from the current permutation. This is crucial for backtracking, allowing us to explore other branches of the decision tree.

The main function will initialize an empty string (or character array) for the current permutation, and a `visited` array. It will then call the recursive helper function.

**Time Complexity:** The number of permutations for a string of length `N` is `N!`. For each permutation, we might spend `O(N)` time to construct it (e.g., copying characters, converting char array to string) and print. Additionally, the backtracking process involves iterating through `N` choices at each level of recursion. Therefore, the overall time complexity is approximately `O(N * N!)`.

**Space Complexity:** The space complexity is `O(N)` due to the recursion stack depth (at most `N` levels) and the auxiliary space required to store the current permutation (also `O(N)` characters) and the boolean `visited` array (`O(N)` space).

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

// Function to print all permutations
void findPermutations(char* str_arr, int n, char* current_perm, bool* visited, int level) {
    // Base case: If the current permutation length equals string length, print it
    if (level == n) {
        current_perm[level] = '\0'; // Null-terminate the string
        printf("%s\n", current_perm);
        return;
    }

    // Recursive step: Try each character from the original string
    for (int i = 0; i < n; i++) {
        // If character at index i has not been visited
        if (!visited[i]) {
            // Choose: Add character to current permutation and mark as visited
            current_perm[level] = str_arr[i];
            visited[i] = true;

            // Explore: Recurse for the next level
            findPermutations(str_arr, n, current_perm, visited, level + 1);

            // Unchoose (Backtrack): Remove character from current permutation and unmark as visited
            visited[i] = false;
        }
    }
}

int main() {
    char s[10]; // Assuming max string length as per constraints + null terminator
    if (scanf("%s", s) != 1) {
        return 1; // Error reading input
    }

    int n = strlen(s);

    char current_perm[10]; // Buffer for current permutation
    bool visited[10];      // Visited array

    // Initialize visited array to all false
    for (int i = 0; i < n; i++) {
        visited[i] = false;
    }

    findPermutations(s, n, current_perm, visited, 0);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

// Function to print all permutations
void findPermutations(const std::string& s, std::string& current_perm, std::vector<bool>& visited) {
    // Base case: If the current permutation length equals string length, print it
    if (current_perm.length() == s.length()) {
        std::cout << current_perm << std::endl;
        return;
    }

    // Recursive step: Try each character from the original string
    for (int i = 0; i < s.length(); ++i) {
        // If character at index i has not been visited
        if (!visited[i]) {
            // Choose: Add character to current permutation and mark as visited
            current_perm.push_back(s[i]);
            visited[i] = true;

            // Explore: Recurse
            findPermutations(s, current_perm, visited);

            // Unchoose (Backtrack): Remove character from current permutation and unmark as visited
            visited[i] = false;
            current_perm.pop_back();
        }
    }
}

int main() {
    std::string s;
    std::cin >> s;

    std::string current_perm;
    std::vector<bool> visited(s.length(), false);

    findPermutations(s, current_perm, visited);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Permutations {

    // Function to print all permutations
    public static void findPermutations(char[] s_chars, StringBuilder currentPerm, boolean[] visited) {
        // Base case: If the current permutation length equals string length, print it
        if (currentPerm.length() == s_chars.length) {
            System.out.println(currentPerm.toString());
            return;
        }

        // Recursive step: Try each character from the original string
        for (int i = 0; i < s_chars.length; i++) {
            // If character at index i has not been visited
            if (!visited[i]) {
                // Choose: Add character to current permutation and mark as visited
                currentPerm.append(s_chars[i]);
                visited[i] = true;

                // Explore: Recurse
                findPermutations(s_chars, currentPerm, visited);

                // Unchoose (Backtrack): Remove character from current permutation and unmark as visited
                currentPerm.deleteCharAt(currentPerm.length() - 1);
                visited[i] = false;
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.next();
        scanner.close();

        char[] s_chars = s.toCharArray();
        StringBuilder currentPerm = new StringBuilder();
        boolean[] visited = new boolean[s_chars.length];

        findPermutations(s_chars, currentPerm, visited);
    }
}
```

## Python Solution
```python
def find_permutations_util(s_chars, current_perm, visited, results):
    # Base case: If the current permutation length equals string length, add it to results
    if len(current_perm) == len(s_chars):
        results.append("".join(current_perm))
        return

    # Recursive step: Try each character from the original string
    for i in range(len(s_chars)):
        # If character at index i has not been visited
        if not visited[i]:
            # Choose: Add character to current permutation and mark as visited
            current_perm.append(s_chars[i])
            visited[i] = True

            # Explore: Recurse
            find_permutations_util(s_chars, current_perm, visited, results)

            # Unchoose (Backtrack): Remove character from current permutation and unmark as visited
            visited[i] = False
            current_perm.pop()

def get_all_permutations(s):
    s_chars = list(s)
    current_perm = []
    visited = [False] * len(s_chars)
    results = []

    find_permutations_util(s_chars, current_perm, visited, results)
    return results

if __name__ == "__main__":
    s = input()
    permutations = get_all_permutations(s)
    for p in permutations:
        print(p)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to print all permutations
function findPermutations(s_chars, currentPerm, visited) {
    // Base case: If the current permutation length equals string length, print it
    if (currentPerm.length === s_chars.length) {
        console.log(currentPerm.join(''));
        return;
    }

    // Recursive step: Try each character from the original string
    for (let i = 0; i < s_chars.length; i++) {
        // If character at index i has not been visited
        if (!visited[i]) {
            // Choose: Add character to current permutation and mark as visited
            currentPerm.push(s_chars[i]);
            visited[i] = true;

            // Explore: Recurse
            findPermutations(s_chars, currentPerm, visited);

            // Unchoose (Backtrack): Remove character from current permutation and unmark as visited
            visited[i] = false;
            currentPerm.pop();
        }
    }
}

rl.on('line', (s) => {
    const s_chars = s.split('');
    const currentPerm = [];
    const visited = new Array(s_chars.length).fill(false);

    findPermutations(s_chars, currentPerm, visited);
    rl.close();
});
```