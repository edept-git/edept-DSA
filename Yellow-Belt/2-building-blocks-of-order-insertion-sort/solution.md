# Solutions for Building Blocks of Order: Insertion Sort

### Approach
Insertion Sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort. However, it has some advantages:

**Algorithm:**
1.  Start from the second element (index 1) of the array. The first element (index 0) is considered to be the 'already sorted' part of the array, as a single element is always sorted.
2.  Take the current element (let's call it `key`).
3.  Compare `key` with the elements in the sorted part, moving from right to left.
4.  If an element in the sorted part is greater than `key`, shift it one position to the right to make space for `key`.
5.  Continue shifting until an element smaller than or equal to `key` is found, or the beginning of the array is reached.
6.  Insert `key` into the empty position.
7.  Repeat steps 2-6 for all remaining unsorted elements until the entire array is sorted.

**Data Structures:**
The primary data structure used is the input array itself. No additional complex data structures are required.

**Time Complexity:**
-   **Worst Case:** O(n^2). This occurs when the array is sorted in reverse order. Each element needs to be compared with and potentially shifted past all preceding elements.
-   **Average Case:** O(n^2). For randomly ordered arrays, the behavior is similar to the worst case.
-   **Best Case:** O(n). This occurs when the array is already sorted. In this scenario, each element is compared only once with its predecessor, and no shifting is required.

**Space Complexity:**
-   O(1). Insertion Sort is an in-place sorting algorithm, meaning it requires only a constant amount of additional memory space for temporary variables (like `key` and loop counters), regardless of the input size.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to perform insertion sort on an array
void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key,
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int n;
    scanf("%d", &n);

    // Dynamically allocate memory for the array
    int *arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        // Handle memory allocation error
        return 1;
    }

    // Read array elements from stdin
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Call the insertion sort function
    insertionSort(arr, n);

    // Print the sorted array to stdout
    for (int i = 0; i < n; i++) {
        printf("%d%s", arr[i], (i == n - 1) ? "" : " ");
    }
    printf("\n");

    // Free the dynamically allocated memory
    free(arr);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
// No specific algorithm header needed for a basic insertion sort implementation

// Function to perform insertion sort on a vector
void insertionSort(std::vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key,
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    // Optimize C++ standard streams for faster input/output
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cin >> n;

    std::vector<int> arr(n);
    // Read array elements into the vector
    for (int i = 0; i < n; i++) {
        std::cin >> arr[i];
    }

    // Call the insertion sort function
    insertionSort(arr);

    // Print the sorted vector to stdout
    for (int i = 0; i < n; i++) {
        std::cout << arr[i] << (i == n - 1 ? "" : " ");
    }
    std::cout << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
// import java.util.Arrays; // Not strictly necessary, manual printing is fine

class Solution {
    // Function to perform insertion sort on an array
    public void insertionSort(int[] arr) {
        int n = arr.length;
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            // Move elements of arr[0..i-1], that are greater than key,
            // to one position ahead of their current position
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] arr = new int[n];
        // Read array elements from stdin
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Create an instance of Solution and call the sorting method
        Solution sol = new Solution();
        sol.insertionSort(arr);

        // Print the sorted array to stdout
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + (i == n - 1 ? "" : " "));
        }
        System.out.println();

        scanner.close(); // Close the scanner to release resources
    }
}
```

## Python Solution
```python
def insertion_sort(arr):
    """
    Performs insertion sort on the given list in-place.
    """
    n = len(arr)
    for i in range(1, n):
        key = arr[i]
        j = i - 1

        # Move elements of arr[0..i-1], that are greater than key,
        # to one position ahead of their current position
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key

def main():
    # Read the number of elements
    n = int(input())
    # Read the array elements as a list of integers
    arr = list(map(int, input().split()))

    # Call the insertion sort function
    insertion_sort(arr)

    # Print the sorted array elements separated by spaces
    print(*(arr))

if __name__ == "__main__":
    main()

```

## JavaScript Solution
```javascript
// Using Node.js standard input/output with the readline module
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];
// Collect all input lines
rl.on('line', (line) => {
    inputLines.push(line);
});

// Once all input is received, process it
rl.on('close', () => {
    main();
});

// Function to perform insertion sort on an array
function insertionSort(arr) {
    let n = arr.length;
    for (let i = 1; i < n; i++) {
        let key = arr[i];
        let j = i - 1;

        // Move elements of arr[0..i-1], that are greater than key,
        // to one position ahead of their current position
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
    return arr; // Array is sorted in-place, return for clarity/chaining
}

function main() {
    // Parse the number of elements from the first line of input
    let n = parseInt(inputLines[0]);
    // Parse the array elements from the second line of input
    let arr = inputLines[1].split(' ').map(Number);

    // Call the insertion sort function
    insertionSort(arr);

    // Print the sorted array elements separated by spaces
    console.log(arr.join(' '));
}
```