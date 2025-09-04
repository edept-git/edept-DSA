# Solutions for Array Sleuth: Find Your Element

### Approach
This problem can be solved using a straightforward approach called Linear Search. The algorithm involves iterating through each element of the array, starting from the first element (index 0), and comparing it with the `target` value. If a match is found at any point, the index of that element is immediately returned. If the loop completes without finding the `target` in the entire array, it means the element is not present, and thus, -1 is returned. This approach uses the array as its primary data structure.

**Time Complexity:** The worst-case time complexity is O(N), where N is the number of elements in the array. This occurs when the `target` element is at the very end of the array or not present at all, requiring a scan of all N elements. The best-case time complexity is O(1) if the `target` is found at the first position. On average, the time complexity remains O(N).

**Space Complexity:** The space complexity is O(1) because the algorithm only uses a few constant extra variables (like loop counters and the target value) regardless of the input array's size. No additional data structures proportional to the input size are allocated.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to perform linear search
int findElement(int arr[], int size, int target) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found
}

int main() {
    int N;
    // Read the size of the array
    if (scanf("%d", &N) != 1) {
        return 1; // Error reading N
    }

    // Allocate memory for the array
    int *arr = (int *)malloc(N * sizeof(int));
    if (arr == NULL) {
        return 1; // Memory allocation failed
    }

    // Read array elements
    for (int i = 0; i < N; i++) {
        if (scanf("%d", &arr[i]) != 1) {
            free(arr); // Free allocated memory before exiting
            return 1; // Error reading array element
        }
    }

    int target;
    // Read the target element
    if (scanf("%d", &target) != 1) {
        free(arr); // Free allocated memory before exiting
        return 1; // Error reading target
    }

    // Call the linear search function
    int result = findElement(arr, N, target);

    // Print the result
    printf("%d\n", result);

    // Free allocated memory
    free(arr);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

// Function to perform linear search
int findElement(const std::vector<int>& arr, int target) {
    for (int i = 0; i < arr.size(); ++i) {
        if (arr[i] == target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int N;
    // Read the size of the array
    std::cin >> N;

    std::vector<int> arr(N);
    // Read array elements
    for (int i = 0; i < N; ++i) {
        std::cin >> arr[i];
    }

    int target;
    // Read the target element
    std::cin >> target;

    // Call the linear search function
    int result = findElement(arr, target);

    // Print the result
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to perform linear search
    public int findElement(int[] arr, int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                return i; // Target found, return its index
            }
        }
        return -1; // Target not found
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the size of the array
        int N = scanner.nextInt();

        int[] arr = new int[N];
        // Read array elements
        for (int i = 0; i < N; i++) {
            arr[i] = scanner.nextInt();
        }

        // Read the target element
        int target = scanner.nextInt();

        // Create an instance of the Solution class
        Solution sol = new Solution();

        // Call the linear search function
        int result = sol.findElement(arr, target);

        // Print the result
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def find_element(arr, target):
    """
    Performs a linear search to find the first occurrence of the target in the array.

    Args:
        arr (list): A list of integers.
        target (int): The integer to search for.

    Returns:
        int: The index of the first occurrence of the target, or -1 if not found.
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Target found, return its index
    return -1  # Target not found

if __name__ == "__main__":
    # Read the size of the array (not strictly necessary for Python list, but good practice for consistency)
    N = int(input())

    # Read array elements
    arr = list(map(int, input().split()))

    # Read the target element
    target = int(input())

    # Call the linear search function
    result = find_element(arr, target)

    # Print the result
    print(result)

```

## JavaScript Solution
```javascript
// For competitive programming environments, input usually comes from stdin
// using the 'readline' module or similar.
// This example assumes a setup where input is read line by line.

let input = "";
process.stdin.on('data', data => {
    input += data;
});

process.stdin.on('end', () => {
    const lines = input.trim().split('\n');

    // The first line is N (size of array), though not strictly used in JS like C/Java
    // const N = parseInt(lines[0]); 

    // The second line contains the array elements
    const arr = lines[1].split(' ').map(Number);

    // The third line contains the target
    const target = parseInt(lines[2]);

    // Call the function and print the result
    console.log(findElement(arr, target));
});

/**
 * Performs a linear search to find the first occurrence of the target in the array.
 * @param {number[]} arr The array of numbers to search in.
 * @param {number} target The number to search for.
 * @returns {number} The index of the first occurrence of the target, or -1 if not found.
 */
function findElement(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found
}
```