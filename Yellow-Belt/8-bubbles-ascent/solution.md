# Solutions for Bubble's Ascent

### Approach
Bubble Sort is a straightforward sorting algorithm. It works by repeatedly stepping through the list to be sorted, comparing each pair of adjacent items and swapping them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted.

The algorithm uses two nested loops. The outer loop runs `n-1` times (where `n` is the number of elements), ensuring that each element eventually 'bubbles up' to its correct sorted position. The inner loop iterates from the beginning of the array up to `n-i-1` (where `i` is the current pass number of the outer loop). In each iteration of the inner loop, it compares `arr[j]` with `arr[j+1]`. If `arr[j]` is greater than `arr[j+1]`, they are swapped. An optimization can be added: if no swaps occur during an entire pass of the inner loop, it means the array is already sorted, and we can break out of the outer loop early.

**Data Structures:** The primary data structure used is a simple array, as the sorting happens directly within the input array.

**Time Complexity:**
*   **Worst-case and Average-case:** O(n^2). This occurs when the array is in reverse order or elements are highly unsorted, as every element might need to be compared and potentially swapped multiple times.
*   **Best-case:** O(n). This occurs if the array is already sorted. With the optimization (checking if any swaps happened in a pass), the algorithm will only make one full pass and realize no swaps are needed.

**Space Complexity:** O(1), as it is an in-place sorting algorithm, meaning it doesn't require extra space proportional to the input size beyond a few temporary variables for swaps.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to swap two integers
void swap(int* xp, int* yp) {
    int temp = *xp;
    *xp = *yp;
    *yp = temp;
}

// Function to perform Bubble Sort
void bubbleSort(int arr[], int n) {
    int i, j;
    int swapped;
    for (i = 0; i < n - 1; i++) {
        swapped = 0;
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(&arr[j], &arr[j + 1]);
                swapped = 1;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (swapped == 0)
            break;
    }
}

// Main function to read input, sort, and print output
int main() {
    int n;
    // Read the number of elements
    if (scanf("%d", &n) != 1 || n <= 0) {
        fprintf(stderr, "Invalid input for array size.\n");
        return 1;
    }

    int* arr = (int*)malloc(n * sizeof(int));
    if (arr == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        return 1;
    }

    // Read the array elements
    for (int i = 0; i < n; i++) {
        if (scanf("%d", &arr[i]) != 1) {
            fprintf(stderr, "Error reading array element.\n");
            free(arr);
            return 1;
        }
    }

    // Perform bubble sort
    bubbleSort(arr, n);

    // Print the sorted array
    for (int i = 0; i < n; i++) {
        printf("%d", arr[i]);
        if (i < n - 1) {
            printf(" ");
        }
    }
    printf("\n");

    free(arr);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Required for std::swap

// Function to perform Bubble Sort on a vector
void bubbleSort(std::vector<int>& arr) {
    int n = arr.size();
    bool swapped;
    for (int i = 0; i < n - 1; ++i) {
        swapped = false;
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                std::swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (!swapped)
            break;
    }
}

// Main function to read input, sort, and print output
int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    // Read the number of elements
    std::cin >> n;

    std::vector<int> arr(n);

    // Read the array elements
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    // Perform bubble sort
    bubbleSort(arr);

    // Print the sorted vector
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

public class Solution {

    // Function to perform Bubble Sort
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j+1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            // If no two elements were swapped by inner loop, then break
            if (!swapped) {
                break;
            }
        }
    }

    // Main method to read input, sort, and print output
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        int n = scanner.nextInt();

        int[] arr = new int[n];

        // Read the array elements
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Perform bubble sort
        bubbleSort(arr);

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
def bubble_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        swapped = False
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                # Swap elements
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        # If no two elements were swapped by inner loop, then break
        if not swapped:
            break

if __name__ == '__main__':
    # Read the number of elements
    n = int(input())

    # Read the array elements
    arr = list(map(int, input().split()))

    # Perform bubble sort
    bubble_sort(arr)

    # Print the sorted array
    print(*arr)
```

## JavaScript Solution
```javascript
// Function to perform Bubble Sort
function bubbleSort(arr) {
    let n = arr.length;
    let swapped;
    for (let i = 0; i < n - 1; i++) {
        swapped = false;
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                let temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (!swapped) {
            break;
        }
    }
    return arr;
}

// Main logic to handle input and output
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let lines = [];
rl.on('line', (line) => {
    lines.push(line);
}).on('close', () => {
    const n = parseInt(lines[0]);
    const arr = lines[1].split(' ').map(Number);

    const sortedArr = bubbleSort(arr);

    console.log(sortedArr.join(' '));
});
```