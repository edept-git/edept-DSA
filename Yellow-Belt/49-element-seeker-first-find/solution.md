# Solutions for Element Seeker: First Find

### Approach
The problem requires us to find the first occurrence of a target element within an array. A straightforward approach for this is **Linear Search**.
The algorithm works as follows:
1. Initialize a loop that iterates through the array from the first element (index 0) up to the last element (index `n-1`).
2. In each iteration, compare the current element `arr[i]` with the `target` value.
3. If `arr[i]` is equal to `target`, it means we have found the target. Since we need the *first* occurrence, we immediately return the current index `i`.
4. If the loop completes without finding the target (i.e., no element matched the `target`), it means the target is not present in the array. In this case, we return `-1`.

**Data Structures:**
The only data structure used is the input array itself. No additional complex data structures are required.

**Time Complexity:**
*   **Worst Case:** O(n), when the target element is at the very end of the array, or not present at all. In these scenarios, the algorithm has to iterate through all `n` elements.
*   **Best Case:** O(1), when the target element is found at the beginning of the array (index 0).
*   **Average Case:** O(n), as on average, we might expect to search about half the array.

**Space Complexity:**
O(1), as the algorithm only uses a few constant extra variables (like loop counters and the target value) regardless of the input array size. No additional memory proportional to the input size is allocated.


## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // For malloc, free

// Function to perform linear search
// Returns the 0-based index of the first occurrence of target, or -1 if not found.
int linearSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found in the array
}

int main() {
    int n;
    // Read the size of the array
    if (scanf("%d", &n) != 1 || n < 1 || n > 1000) {
        fprintf(stderr, "Invalid array size.\n");
        return 1;
    }

    // Allocate memory for the array
    int* arr = (int*)malloc(n * sizeof(int));
    if (arr == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        return 1;
    }

    // Read array elements
    for (int i = 0; i < n; i++) {
        if (scanf("%d", &arr[i]) != 1) {
            fprintf(stderr, "Failed to read array element.\n");
            free(arr);
            return 1;
        }
    }

    int target;
    // Read the target value
    if (scanf("%d", &target) != 1) {
        fprintf(stderr, "Failed to read target value.\n");
        free(arr);
        return 1;
    }

    // Call the linear search function
    int result = linearSearch(arr, n, target);

    // Print the result
    printf("%d\n", result);

    // Free the allocated memory
    free(arr);

    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <vector> // For std::vector

// Function to perform linear search
// Returns the 0-based index of the first occurrence of target, or -1 if not found.
int linearSearch(const std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found in the array
}

int main() {
    std::ios_base::sync_with_stdio(false); // Optimize C++ standard streams
    std::cin.tie(NULL); // Untie cin from cout

    int n;
    // Read the size of the array
    if (!(std::cin >> n) || n < 1 || n > 1000) {
        std::cerr << "Invalid array size." << std::endl;
        return 1;
    }

    // Read array elements into a std::vector
    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        if (!(std::cin >> arr[i])) {
            std::cerr << "Failed to read array element." << std::endl;
            return 1;
        }
    }

    int target;
    // Read the target value
    if (!(std::cin >> target)) {
        std::cerr << "Failed to read target value." << std::endl;
        return 1;
    }

    // Call the linear search function
    int result = linearSearch(arr, target);

    // Print the result
    std::cout << result << std::endl;

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to perform linear search
    // Returns the 0-based index of the first occurrence of target, or -1 if not found.
    public static int linearSearch(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i; // Target found, return its index
            }
        }
        return -1; // Target not found in the array
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the size of the array
        int n = scanner.nextInt();
        if (n < 1 || n > 1000) {
            System.err.println("Invalid array size.");
            scanner.close();
            return;
        }

        // Read array elements
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Read the target value
        int target = scanner.nextInt();

        // Call the linear search function
        int result = linearSearch(arr, target);

        // Print the result
        System.out.println(result);

        scanner.close();
    }
}

```

## Python Solution
```python
import sys

def linear_search(arr, target):
    """
    Performs linear search to find the first occurrence of target in arr.
    Returns the 0-based index of the first occurrence, or -1 if not found.
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Target found, return its index
    return -1  # Target not found in the array

def main():
    # Read the size of the array
    n = int(input())
    if not (1 <= n <= 1000):
        print("Invalid array size.", file=sys.stderr)
        sys.exit(1)

    # Read array elements
    arr = list(map(int, input().split()))
    if len(arr) != n:
        print("Number of array elements does not match declared size.", file=sys.stderr)
        sys.exit(1)

    # Read the target value
    target = int(input())

    # Call the linear search function
    result = linear_search(arr, target)

    # Print the result
    print(result)

if __name__ == "__main__":
    main()

```

## JavaScript Solution
```javascript
// Function to perform linear search
// Returns the 0-based index of the first occurrence of target, or -1 if not found.
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found in the array
}

// Main execution logic for handling input/output
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let inputLines = [];
    rl.on('line', (line) => {
        inputLines.push(line);
    });

    rl.on('close', () => {
        let lineIndex = 0;

        // Read the size of the array
        const n = parseInt(inputLines[lineIndex++]);
        if (isNaN(n) || n < 1 || n > 1000) {
            console.error("Invalid array size.");
            process.exit(1);
        }

        // Read array elements
        const arr = inputLines[lineIndex++].split(' ').map(Number);
        if (arr.length !== n) {
            console.error("Number of array elements does not match declared size.");
            process.exit(1);
        }

        // Read the target value
        const target = parseInt(inputLines[lineIndex++]);
        if (isNaN(target)) {
            console.error("Invalid target value.");
            process.exit(1);
        }

        // Call the linear search function
        const result = linearSearch(arr, target);

        // Print the result
        console.log(result);
    });
}

main();

```