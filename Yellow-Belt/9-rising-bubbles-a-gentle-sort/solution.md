# Solutions for Rising Bubbles: A Gentle Sort

### Approach
The Bubble Sort algorithm iterates through the array multiple times. In each iteration, it compares adjacent elements. If an element is greater than its right neighbor, they are swapped. This process effectively 'bubbles up' the largest unsorted element to its correct position at the end of the unsorted portion of the array. This outer pass repeats `N-1` times, where `N` is the number of elements in the array. An optimization can be added: if no swaps occur during an entire pass, it means the array is already sorted, and we can terminate early. The data structure used is a simple array. The time complexity of Bubble Sort is O(N^2) in the worst and average cases, as it involves nested loops that iterate up to N times. In the best case (when the array is already sorted and the optimization is used), the time complexity is O(N) because it only requires one pass to confirm no swaps are needed. The space complexity is O(1) because the sorting is done in-place, without requiring additional data structures proportional to the input size.

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>

// Function to perform Bubble Sort on an array
void bubbleSort(int arr[], int n) {
    bool swapped;
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - 1 - i; j++) {
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

int main() {
    int n;
    // Read the number of elements
    scanf("%d", &n);

    int arr[n]; // Declare array of size n
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
            printf(" ");
        }
    }
    printf("\n");

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
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                std::swap(arr[j], arr[j + 1]);
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
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    // Read the number of elements
    std::cin >> n;

    std::vector<int> arr(n);
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

public class Solution {

    // Function to perform Bubble Sort on an array
    public void bubbleSort(int[] arr) {
        int n = arr.length;
        boolean swapped;
        for (int i = 0; i < n - 1; i++) {
            swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
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

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        int n = scanner.nextInt();

        int[] arr = new int[n];
        // Read the array elements
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Create an instance of Solution to call the bubbleSort method
        Solution sol = new Solution();
        sol.bubbleSort(arr);

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
        for j in range(n - 1 - i):
            if arr[j] > arr[j + 1]:
                # Swap elements
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
                swapped = True
        # If no two elements were swapped by inner loop, then break
        if not swapped:
            break

def main():
    # Read the number of elements
    n = int(input())

    # Read the array elements
    arr = list(map(int, input().split()))

    # Call the bubble_sort function
    bubble_sort(arr)

    # Print the sorted array
    print(*arr)

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to perform Bubble Sort on an array
function bubbleSort(arr) {
    const n = arr.length;
    let swapped;
    for (let i = 0; i < n - 1; i++) {
        swapped = false;
        for (let j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
                swapped = true;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (!swapped) {
            break;
        }
    }
}

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    // Read the number of elements
    const n = parseInt(inputLines[0]);

    // Read the array elements
    const arr = inputLines[1].split(' ').map(Number);

    // Call the bubbleSort function
    bubbleSort(arr);

    // Print the sorted array
    console.log(arr.join(' '));
});
```