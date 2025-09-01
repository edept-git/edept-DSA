# Solutions for The Minimalist's Sort: Finding Order One Swap at a Time

### Approach
The problem requires sorting an array using the Selection Sort algorithm. Selection Sort is an in-place comparison sorting algorithm. It divides the input list into two parts: a sorted sublist of items built up from left to right at the front (left end) of the list, and a sublist of the remaining unsorted items that occupy the rest of the list. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list.

The algorithm proceeds as follows:
1. Iterate from the first element to the second-to-last element of the array. Let's call the current index `i`.
2. In each iteration, assume the element at index `i` is the minimum in the unsorted sub-array.
3. Iterate from `i + 1` to the end of the array to find the actual minimum element in the unsorted part. Keep track of the index of this minimum element, let's call it `minIndex`.
4. If `minIndex` is not equal to `i` (meaning a smaller element was found), swap the element at `arr[i]` with the element at `arr[minIndex]`. This places the smallest element found in the current pass at its correct sorted position.
5. After `n-1` passes, the array will be sorted.

For data structures, a simple array (or dynamic array/vector in some languages) is sufficient. No additional complex data structures are needed as it's an in-place sort.

The time complexity of Selection Sort is O(N^2), where N is the number of elements in the array. This is because there are two nested loops. The outer loop runs `N-1` times, and the inner loop runs approximately `N`, `N-1`, ..., `1` times. The total number of comparisons is roughly `N * (N-1) / 2`, which is proportional to `N^2`. While the number of swaps is only O(N), the dominant factor for time complexity remains the comparisons. The space complexity is O(1) because it sorts the array in-place without requiring any auxiliary data structures proportional to the input size.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // For malloc and free

// Function to swap two elements
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to perform Selection Sort
void selectionSort(int arr[], int n) {
    int i, j, min_idx;

    // One by one move boundary of unsorted subarray
    for (i = 0; i < n - 1; i++) {
        // Find the minimum element in unsorted array
        min_idx = i;
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }

        // Swap the found minimum element with the first element of the unsorted part
        swap(&arr[min_idx], &arr[i]);
    }
}

// Function to print an array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++) {
        printf("%d", arr[i]);
        if (i < size - 1) {
            printf(" ");
        }
    }
    printf("\n");
}

int main() {
    int n;
    // Read the number of elements
    if (scanf("%d", &n) != 1 || n <= 0) {
        // Handle invalid input for n
        fprintf(stderr, "Error: Invalid array size. Must be a positive integer.\n");
        return 1; 
    }

    int* arr = (int*)malloc(n * sizeof(int));
    if (arr == NULL) {
        // Handle memory allocation failure
        fprintf(stderr, "Error: Memory allocation failed.\n");
        return 1;
    }

    // Read array elements
    for (int i = 0; i < n; i++) {
        if (scanf("%d", &arr[i]) != 1) {
            // Handle invalid input for array element
            fprintf(stderr, "Error: Invalid input for array element at index %d.\n", i);
            free(arr);
            return 1;
        }
    }

    // Perform Selection Sort
    selectionSort(arr, n);

    // Print the sorted array
    printArray(arr, n);

    // Free the dynamically allocated memory
    free(arr);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::swap

// Function to perform Selection Sort
void selectionSort(std::vector<int>& arr) {
    int n = arr.size();

    // One by one move boundary of unsorted subarray
    for (int i = 0; i < n - 1; ++i) {
        // Find the minimum element in unsorted array
        int min_idx = i;
        for (int j = i + 1; j < n; ++j) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }

        // Swap the found minimum element with the first element of the unsorted part
        std::swap(arr[min_idx], arr[i]);
    }
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    // Read the number of elements
    if (!(std::cin >> n) || n <= 0) {
        std::cerr << "Error: Invalid array size. Must be a positive integer." << std::endl;
        return 1; 
    }

    std::vector<int> arr(n);

    // Read array elements
    for (int i = 0; i < n; ++i) {
        if (!(std::cin >> arr[i])) {
            std::cerr << "Error: Invalid input for array element at index " << i << "." << std::endl;
            return 1;
        }
    }

    // Perform Selection Sort
    selectionSort(arr);

    // Print the sorted array
    for (int i = 0; i < n; ++i) {
        std::cout << arr[i];
        if (i < n - 1) {
            std::cout << " ";
        }
    }
    std::cout << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.Arrays;

public class Main {

    // Function to perform Selection Sort
    public static void selectionSort(int[] arr) {
        int n = arr.length;

        // One by one move boundary of unsorted subarray
        for (int i = 0; i < n - 1; i++) {
            // Find the minimum element in unsorted array
            int min_idx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[min_idx]) {
                    min_idx = j;
                }
            }

            // Swap the found minimum element with the first element of the unsorted part
            int temp = arr[min_idx];
            arr[min_idx] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        if (!scanner.hasNextInt()) {
            System.err.println("Error: Invalid input. Expected an integer for array size.");
            scanner.close();
            return;
        }
        int n = scanner.nextInt();

        if (n <= 0) {
            System.err.println("Error: Array size must be positive.");
            scanner.close();
            return;
        }

        int[] arr = new int[n];

        // Read array elements
        for (int i = 0; i < n; i++) {
            if (!scanner.hasNextInt()) {
                System.err.println("Error: Invalid input. Expected an integer for array element at index " + i + ".");
                scanner.close();
                return;
            }
            arr[i] = scanner.nextInt();
        }

        // Perform Selection Sort
        selectionSort(arr);

        // Print the sorted array
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i]);
            if (i < n - 1) {
                System.out.print(" ");
            }
        }
        System.out.println();

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

def selection_sort(arr: list[int]) -> None:
    """
    Sorts an array in ascending order using the Selection Sort algorithm.
    Modifies the input array in-place.
    """
    n = len(arr)

    # One by one move boundary of unsorted subarray
    for i in range(n - 1):
        # Find the minimum element in unsorted array
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j

        # Swap the found minimum element with the first element of the unsorted part
        arr[min_idx], arr[i] = arr[i], arr[min_idx]

if __name__ == "__main__":
    try:
        # Read the number of elements
        n_str = sys.stdin.readline().strip()
        if not n_str:
            sys.stderr.write("Error: Empty input for array size.\n")
            sys.exit(1)
        n = int(n_str)
        
        if n <= 0:
            sys.stderr.write("Error: Array size must be positive.\n")
            sys.exit(1)

        # Read array elements
        arr_str = sys.stdin.readline().strip()
        if not arr_str and n > 0:
            sys.stderr.write(f"Error: Expected {n} elements but received an empty line for elements.\n")
            sys.exit(1)
            
        arr = list(map(int, arr_str.split()))

        if len(arr) != n:
            sys.stderr.write(f"Error: Expected {n} elements, but got {len(arr)}.\n")
            sys.exit(1)

        # Perform Selection Sort
        selection_sort(arr);

        # Print the sorted array
        sys.stdout.write(" ".join(map(str, arr)) + "\n")
    except ValueError as e:
        sys.stderr.write(f"Error: Invalid input format. {e}\n")
        sys.exit(1)
    except Exception as e:
        sys.stderr.write(f"An unexpected error occurred: {e}\n")
        sys.exit(1)

```

## JavaScript Solution
```javascript
function selectionSort(arr) {
    const n = arr.length;

    // One by one move boundary of unsorted subarray
    for (let i = 0; i < n - 1; i++) {
        // Find the minimum element in unsorted array
        let min_idx = i;
        for (let j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }

        // Swap the found minimum element with the first element of the unsorted part
        // Using a temporary variable for swap
        let temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
    return arr; // Return the sorted array (though it's sorted in-place)
}

// Node.js specific I/O handling
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
    try {
        if (inputLines.length < 2) {
            console.error("Error: Not enough input lines. Expected array size and elements.");
            process.exit(1);
        }

        const n = parseInt(inputLines[0]);
        if (isNaN(n) || n <= 0) {
            console.error("Error: Invalid array size. Must be a positive integer.");
            process.exit(1);
        }

        const arr = inputLines[1].split(' ').map(Number);

        if (arr.length !== n) {
            console.error(`Error: Expected ${n} elements, but got ${arr.length}.`);
            process.exit(1);
        }
        
        // Check if any element mapping resulted in NaN
        const hasNaN = arr.some(isNaN);
        if (hasNaN) {
            console.error("Error: Invalid array elements. All elements must be numbers.");
            process.exit(1);
        }

        const sortedArr = selectionSort(arr);
        console.log(sortedArr.join(' '));

    } catch (error) {
        console.error(`An unexpected error occurred: ${error.message}`);
        process.exit(1);
    }
});
```