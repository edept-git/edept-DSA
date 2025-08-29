# Solutions for Array Mirror: Reverse and Print

### Approach
The problem requires us to read `N` integers and print them in reverse. The most straightforward approach involves two main steps. First, we declare a 1D array (or an equivalent dynamic list/vector in some languages) of size `N`. Then, we use a loop to read each of the `N` integers and store them sequentially into this array. After all elements are stored, we use a second loop to traverse the array from the last element (index `N-1`) down to the first element (index `0`), printing each element as we go, followed by a space. Finally, we print a newline character to complete the output. This approach uses an array to store all elements, requiring O(N) space. Both the reading and printing phases involve iterating through the array once, leading to an overall time complexity of O(N).

## C Solution
```c
#include <stdio.h>

// Function to print array elements in reverse order
void reverseAndPrint(int arr[], int n) {
    for (int i = n - 1; i >= 0; i--) {
        printf("%d", arr[i]);
        if (i > 0) {
            printf(" "); // Print space between numbers
        }
    }
    printf("\n"); // Print newline at the end
}

int main() {
    int n;
    // Read N
    scanf("%d", &n);

    // Declare an array of size N
    // For C, using a Variable Length Array (VLA) or dynamic allocation is common for variable N.
    // VLA is standard in C99, but not C++ standard. For competitive programming, usually allowed.
    // Alternative: int* arr = (int*)malloc(n * sizeof(int));
    int arr[n]; 

    // Read N integers into the array
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Call the function to reverse and print
    reverseAndPrint(arr, n);

    // If using malloc, remember to free the memory:
    // free(arr);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::reverse if needed, but manual loop is fine

// Function to print vector elements in reverse order
void reverseAndPrint(const std::vector<int>& arr) {
    // Iterate from the last element to the first
    for (int i = arr.size() - 1; i >= 0; --i) {
        std::cout << arr[i];
        if (i > 0) {
            std::cout << " "; // Print space between numbers
        }
    }
    std::cout << std::endl; // Print newline at the end
}

int main() {
    std::ios_base::sync_with_stdio(false); // Optimize C++ streams for faster I/O
    std::cin.tie(NULL);

    int n;
    // Read N
    std::cin >> n;

    // Declare a vector of size N
    std::vector<int> arr(n);

    // Read N integers into the vector
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    // Call the function to reverse and print
    reverseAndPrint(arr);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to print array elements in reverse order
    public static void reverseAndPrint(int[] arr) {
        // Iterate from the last element to the first
        for (int i = arr.length - 1; i >= 0; i--) {
            System.out.print(arr[i]);
            if (i > 0) {
                System.out.print(" "); // Print space between numbers
            }
        }
        System.out.println(); // Print newline at the end
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read N
        int n = scanner.nextInt();

        // Declare an array of size N
        int[] arr = new int[n];

        // Read N integers into the array
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Call the function to reverse and print
        reverseAndPrint(arr);

        scanner.close();
    }
}
```

## Python Solution
```python
def reverse_and_print(arr):
    # Iterate from the last element to the first and print
    # Using join for efficient printing with spaces
    reversed_elements = [str(arr[i]) for i in range(len(arr) - 1, -1, -1)]
    print(" ".join(reversed_elements))

def main():
    # Read N
    n = int(input())

    # Read N integers into a list
    # map(int, input().split()) reads a line of space-separated integers
    # and converts them to integers, then creates a list.
    arr = list(map(int, input().split()))

    # Call the function to reverse and print
    reverse_and_print(arr)

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
process.stdin.resume();
process.stdin.setEncoding('utf-8');

let inputString = '';
let currentLine = 0;

process.stdin.on('data', inputStdin => {
    inputString += inputStdin;
});

process.stdin.on('end', _ => {
    inputString = inputString.trim().split('\n').map(str => str.trim());
    main();
});

function readLine() {
    return inputString[currentLine++];
}

// Function to print array elements in reverse order
function reverseAndPrint(arr) {
    // Create a new array to store elements in reverse
    let reversedArr = [];
    for (let i = arr.length - 1; i >= 0; i--) {
        reversedArr.push(arr[i]);
    }
    // Join the reversed elements with spaces and print
    console.log(reversedArr.join(' '));
}

function main() {
    // Read N
    const n = parseInt(readLine(), 10);

    // Read N integers into an array
    const arr = readLine().split(' ').map(arrTemp => parseInt(arrTemp, 10));

    // Call the function to reverse and print
    reverseAndPrint(arr);
}
```