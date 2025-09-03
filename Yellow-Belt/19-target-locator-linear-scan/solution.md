# Solutions for Target Locator: Linear Scan

### Approach
The most straightforward way to solve this problem is using a linear search algorithm. The algorithm involves iterating through each element of the array, one by one, starting from the first element (index 0) up to the last element. In each step of the iteration, we compare the current array element with the `target` value. If a match is found, we immediately return the current index, as we are looking for the *first* occurrence. If the loop completes without finding the `target` in any of the elements, it means the `target` is not present in the array, and we should return `-1`. This approach uses an array as its primary data structure. The time complexity for this algorithm is O(N) in the worst-case scenario (when the target is at the end of the array or not present at all) because, in the worst case, we might need to check every single element. The best-case time complexity is O(1) if the target is the very first element. The space complexity is O(1) because we only use a few constant extra variables (like loop counters and the target value) regardless of the array's size.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to perform linear search
int linearSearch(int arr[], int n, int target) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found
}

int main() {
    int n;
    // Read the size of the array
    if (scanf("%d", &n) != 1 || n <= 0) {
        fprintf(stderr, "Invalid array size.\n");
        return 1;
    }

    int *arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        return 1;
    }

    // Read array elements
    for (int i = 0; i < n; i++) {
        if (scanf("%d", &arr[i]) != 1) {
            fprintf(stderr, "Invalid array element.\n");
            free(arr);
            return 1;
        }
    }

    int target;
    // Read the target element
    if (scanf("%d", &target) != 1) {
        fprintf(stderr, "Invalid target element.\n");
        free(arr);
        return 1;
    }

    // Call the linear search function
    int result = linearSearch(arr, n, target);

    // Print the result
    printf("%d\n", result);

    free(arr); // Free allocated memory
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

// Function to perform linear search
int linearSearch(const std::vector<int>& arr, int target) {
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

    int n;
    // Read the size of the array
    std::cin >> n;
    if (n <= 0) {
        std::cerr << "Invalid array size.\n";
        return 1;
    }

    std::vector<int> arr(n);
    // Read array elements
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    int target;
    // Read the target element
    std::cin >> target;

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
    public static int linearSearch(int[] arr, int target) {
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
        int n = scanner.nextInt();
        if (n <= 0) {
            System.err.println("Invalid array size.");
            scanner.close();
            return;
        }

        int[] arr = new int[n];
        // Read array elements
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Read the target element
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
    Performs a linear search to find the target in the array.
    Returns the index of the target if found, otherwise -1.
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Target found, return its index
    return -1  # Target not found

if __name__ == "__main__":
    # Read the size of the array
    try:
        n = int(input())
    except ValueError:
        print("Invalid array size.", file=sys.stderr)
        sys.exit(1)

    if n <= 0:
        print("Invalid array size.", file=sys.stderr)
        sys.exit(1)

    arr = []
    # Read array elements one by one
    for _ in range(n):
        try:
            arr.append(int(input()))
        except ValueError:
            print("Invalid array element.", file=sys.stderr)
            sys.exit(1)

    # Read the target element
    try:
        target = int(input())
    except ValueError:
        print("Invalid target element.", file=sys.stderr)
        sys.exit(1)

    # Call the linear search function
    result = linear_search(arr, target)

    # Print the result
    print(result)
```

## JavaScript Solution
```javascript
// Function to perform linear search
function linearSearch(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i; // Target found, return its index
        }
    }
    return -1; // Target not found
}

// Main execution part for Node.js environment
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let input = [];
rl.on('line', (line) => {
    input.push(line);
}).on('close', () => {
    let lineIdx = 0;

    // Read the size of the array
    const n = parseInt(input[lineIdx++]);
    if (isNaN(n) || n <= 0) {
        console.error("Invalid array size.");
        process.exit(1);
    }

    let arr = [];
    // Read array elements
    for (let i = 0; i < n; i++) {
        const num = parseInt(input[lineIdx++]);
        if (isNaN(num)) {
            console.error("Invalid array element.");
            process.exit(1);
        }
        arr.push(num);
    }

    // Read the target element
    const target = parseInt(input[lineIdx++]);
    if (isNaN(target)) {
        console.error("Invalid target element.");
        process.exit(1);
    }

    // Call the linear search function
    const result = linearSearch(arr, target);

    // Print the result
    console.log(result);
});
```