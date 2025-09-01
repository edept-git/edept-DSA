# Solutions for Bubble Up! Sort an Array

### Approach
The Bubble Sort algorithm works by iterating through the array multiple times. In each iteration, it compares adjacent elements and swaps them if they are in the wrong order (i.e., the left element is greater than the right element for ascending sort). This process effectively "bubbles" the largest unsorted element to its correct position at the end of the unsorted portion of the array. The outer loop runs `N-1` times, where `N` is the number of elements, to ensure all elements are placed correctly. The inner loop iterates from the beginning of the unsorted portion up to the last unsorted element. An optimization can be added to stop the algorithm early if no swaps are made in a particular pass, indicating the array is already sorted.
The algorithm uses no additional data structures beyond the input array itself for sorting, making it an in-place sorting algorithm.

**Time Complexity:** In the worst-case and average-case scenarios (e.g., reverse-sorted array), Bubble Sort performs approximately `N^2/2` comparisons and swaps, leading to a time complexity of O(N^2). In the best-case scenario (already sorted array with the optimization), it performs N-1 comparisons in the first pass and exits, resulting in O(N) time complexity.

**Space Complexity:** Bubble Sort is an in-place sorting algorithm, requiring only a constant amount of extra space for temporary variables (like a swap variable). Thus, its space complexity is O(1).

## C Solution
```c
#include <stdio.h>
#include <stdbool.h> // For bool type

// Function to perform Bubble Sort on an array
void bubbleSort(int arr[], int n) {
    bool swapped;
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - 1 - i; j++) {
            // Compare adjacent elements
            if (arr[j] > arr[j+1]) {
                // Swap them if they are in the wrong order
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
                swapped = true;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (swapped == false) {
            break;
        }
    }
}

int main() {
    int n;
    // Read the number of elements
    scanf("%d", &n);

    int arr[n]; // Declare array of size n (VLA, C99)

    // Read the array elements
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Call the bubbleSort function
    bubbleSort(arr, n);

    // Print the sorted array
    for (int i = 0; i < n; i++) {
        printf("%d", arr[i]);
        if (i < n - 1) {
            printf(" "); // Print space between elements
        }
    }
    printf("\n"); // Print newline at the end

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::swap

// Function to perform Bubble Sort on a vector
void bubbleSort(std::vector<int>& arr) {
    int n = arr.size();
    bool swapped;
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - 1 - i; j++) {
            // Compare adjacent elements
            if (arr[j] > arr[j+1]) {
                // Swap them if they are in the wrong order
                std::swap(arr[j], arr[j+1]);
                swapped = true;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (!swapped) {
            break;
        }
    }
}

int main() {
    std::ios_base::sync_with_stdio(false); // Optimize C++ standard streams
    std::cin.tie(NULL);                   // Untie cin from cout

    int n;
    // Read the number of elements
    std::cin >> n;

    std::vector<int> arr(n); // Declare a vector of size n

    // Read the vector elements
    for (int i = 0; i < n; i++) {
        std::cin >> arr[i];
    }

    // Call the bubbleSort function
    bubbleSort(arr);

    // Print the sorted vector
    for (int i = 0; i < n; i++) {
        std::cout << arr[i];
        if (i < n - 1) {
            std::cout << " "; // Print space between elements
        }
    }
    std::cout << std::endl; // Print newline at the end

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to perform Bubble Sort on an array
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
                // Compare adjacent elements
                if (arr[j] > arr[j+1]) {
                    // Swap them if they are in the wrong order
                    int temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] = temp;
                    swapped = true;
                }
            }
            // If no two elements were swapped by inner loop, then break
            if (!swapped) {
                break;
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        int n = scanner.nextInt();

        int[] arr = new int[n]; // Declare an array of size n

        // Read the array elements
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Call the bubbleSort function
        bubbleSort(arr);

        // Print the sorted array
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i]);
            if (i < n - 1) {
                System.out.print(" "); // Print space between elements
            }
        }
        System.out.println(); // Print newline at the end

        scanner.close(); // Close the scanner
    }
}
```

## Python Solution
```python
def bubble_sort(arr):
    n = len(arr)
    # Traverse through all array elements
    for i in range(n - 1):
        swapped = False
        # Last i elements are already in place
        for j in range(0, n - 1 - i):
            # Traverse the array from 0 to n-i-1
            # Swap if the element found is greater than the next element
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        # If no two elements were swapped by inner loop, then break
        if not swapped:
            break
    return arr

if __name__ == "__main__":
    # Read the number of elements
    n = int(input())
    
    # Read the array elements as a list of integers
    arr = list(map(int, input().split()))

    # Call the bubble_sort function
    sorted_arr = bubble_sort(arr)

    # Print the sorted array
    print(*(sorted_arr))
```

## JavaScript Solution
```javascript
// Function to perform Bubble Sort on an array
function bubbleSort(arr) {
    const n = arr.length;
    let swapped;
    for (let i = 0; i < n - 1; i++) {
        swapped = false;
        for (let j = 0; j < n - 1 - i; j++) {
            // Compare adjacent elements
            if (arr[j] > arr[j+1]) {
                // Swap them if they are in the wrong order
                let temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
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

// Standard input/output for competitive programming environments (Node.js)
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
    // The first line is N, the number of elements
    const n = parseInt(inputLines[0]);
    
    // The second line contains the array elements
    const arr = inputLines[1].split(' ').map(Number);

    // Call the bubbleSort function
    const sortedArr = bubbleSort(arr);

    // Print the sorted array, space-separated
    console.log(sortedArr.join(' '));
});
```