# Solutions for Element Explorer: Locate Your Target

### Approach
The linear search algorithm is a straightforward method for finding an element within a list or array. The approach involves iterating through each element of the array, one by one, starting from the beginning. In each step of the iteration, we compare the current element with the `target` value we are looking for. If a match is found, we immediately return the current index of that element. If the loop completes its traversal of the entire array without finding the `target` element, it means the element is not present in the array, and we return `-1` to indicate this. This algorithm primarily uses an array as its data structure.

The time complexity of linear search is O(N) in the worst-case scenario, where N is the number of elements in the array. This occurs if the target element is at the very end of the array or not present at all, requiring a scan of all N elements. In the best-case scenario (target at the first position), it's O(1). The space complexity is O(1) because it only uses a constant amount of extra space for variables like loop counters and temporary storage, regardless of the input array size.


## C Solution
```c
#include <stdio.h>

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
    scanf("%d", &n);

    int arr[n]; // Declare array of size n (VLA - C99 feature)
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
    // Read the size of the array
    std::cin >> n;

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

public class Solution {

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
def linear_search(arr, target):
    """
    Function to perform linear search.
    :param arr: List of integers to search within.
    :param target: The integer to search for.
    :return: The index of the first occurrence of the target, or -1 if not found.
    """
    for i in range(len(arr)):
        if arr[i] == target:
            return i  # Target found, return its index
    return -1  # Target not found

if __name__ == "__main__":
    # Read the size of the array
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

let inputLines = [];

rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    // Function to perform linear search
    function linearSearch(arr, target) {
        for (let i = 0; i < arr.length; i++) {
            if (arr[i] === target) {
                return i; // Target found, return its index
            }
        }
        return -1; // Target not found
    }

    // Parse input
    const n = parseInt(inputLines[0]);
    const arr = inputLines[1].split(' ').map(Number);
    const target = parseInt(inputLines[2]);

    // Call the linear search function
    const result = linearSearch(arr, target);

    // Print the result
    console.log(result);
});

```