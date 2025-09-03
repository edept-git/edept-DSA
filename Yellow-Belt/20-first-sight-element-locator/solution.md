# Solutions for First Sight: Element Locator

### Approach
The problem can be solved using a simple linear search algorithm. We iterate through the array from the beginning (index 0) to the end. In each step, we compare the current element with the target value. If a match is found, we immediately return the current index, as we are looking for the *first* occurrence. If the loop completes without finding the target value, it means the target is not present in the array, so we return -1. This approach directly checks each element sequentially.

*   **Algorithm**:
    1.  Initialize a loop counter `i` from 0 to `N-1` (where `N` is the array size).
    2.  In each iteration, compare `array[i]` with the `target`.
    3.  If `array[i]` equals `target`, return `i`.
    4.  If the loop finishes without returning, it means `target` was not found. Return -1.

*   **Data Structures**: The primary data structure used is a simple array (or list). No auxiliary data structures are required.

*   **Time Complexity**: In the worst-case scenario (the target element is at the very end of the array, or not present at all), we might have to check every element once. This gives a time complexity of O(N), where N is the number of elements in the array. In the best case (target is the first element), it's O(1).

*   **Space Complexity**: The algorithm uses a constant amount of extra space for variables like the loop counter and the target value, regardless of the array size. Hence, the space complexity is O(1).

## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // Required for malloc and free

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
    // Read the number of elements
    scanf("%d", &n);

    // Dynamically allocate memory for the array
    int *arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        return 1; // Memory allocation failed
    }

    // Read array elements
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int target;
    // Read the target element
    scanf("%d", &target);

    // Call the linear search function
    int result = linearSearch(arr, n, target);

    // Print the result
    printf("%d\n", result);

    // Free the dynamically allocated memory
    free(arr);

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
    int n;
    // Read the number of elements
    std::cin >> n;

    // Create a vector and read elements
    std::vector<int> arr(n);
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

        // Read the number of elements
        int n = scanner.nextInt();

        // Create an array and read elements
        int[] arr = new int[n];
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
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Target found, return its index
    return -1  # Target not found

if __name__ == "__main__":
    # Read the number of elements
    n = int(input())

    # Read array elements
    arr = list(map(int, input().split()))

    # Read the target element
    target = int(input())

    # Call the linear search function
    result = linear_search(arr, target)

    # Print the result
    print(result)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let input = [];

rl.on('line', (line) => {
    input.push(line);
}).on('close', () => {
    // Function to perform linear search
    function linearSearch(arr, target) {
        for (let i = 0; i < arr.length; i++) {
            if (arr[i] === target) {
                return i; // Target found, return its index
            }
        }
        return -1; // Target not found
    }

    const n = parseInt(input[0]);
    const arr = input[1].split(' ').map(Number);
    const target = parseInt(input[2]);

    const result = linearSearch(arr, target);
    console.log(result);
});
```