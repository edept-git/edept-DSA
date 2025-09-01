# Solutions for Array's Top Score: Find the Max!

### Approach
The most straightforward way to find the maximum element in an array is to iterate through each element once. We can start by assuming the first element of the array is the maximum. Then, we go through the rest of the array, comparing each element with our current maximum. If we find an element that is larger than our current maximum, we update our maximum to that new element. After checking every element in the array, the value we have stored as our maximum will indeed be the true maximum element of the array.

This approach uses an array as its primary data structure.
The **time complexity** for this algorithm is O(N), where N is the number of elements in the array. This is because, in the worst case (and typically), we need to visit every single element in the array exactly once to ensure we haven't missed a larger value.
The **space complexity** is O(1) because we only use a few fixed-size variables (like `max_val` and a loop counter) regardless of how large the input array is. We don't create any new data structures that grow with the input size.

## C Solution
```c
#include <stdio.h>
#include <limits.h> // Required for INT_MIN if n can be 0, though constraints say n >= 1

// Function to find the maximum element in an array
int findMax(int arr[], int n) {
    // Constraint N >= 1 ensures arr is not empty
    int max_val = arr[0]; // Initialize max_val with the first element
    for (int i = 1; i < n; i++) {
        if (arr[i] > max_val) {
            max_val = arr[i]; // Update if a larger element is found
        }
    }
    return max_val;
}

int main() {
    int n;
    // Read the number of elements
    scanf("%d", &n);

    // Declare an array of size n (max N is 1000 as per constraints)
    int arr[1000]; 

    // Read elements into the array
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Call the function to find the maximum element
    int result = findMax(arr, n);

    // Print the result
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Not strictly needed for manual loop, but good for std::max if used

// Function to find the maximum element in a vector
int findMax(const std::vector<int>& arr) {
    // Constraint N >= 1 ensures arr is not empty
    int max_val = arr[0]; // Initialize max_val with the first element
    for (size_t i = 1; i < arr.size(); ++i) {
        if (arr[i] > max_val) {
            max_val = arr[i]; // Update if a larger element is found
        }
    }
    return max_val;
    // Alternative using STL (might be too advanced for White Belt explanation):
    // return *std::max_element(arr.begin(), arr.end());
}

int main() {
    std::ios_base::sync_with_stdio(false); // Optimize C++ standard streams
    std::cin.tie(NULL);                   // Untie cin from cout

    int n;
    // Read the number of elements
    std::cin >> n;

    std::vector<int> arr(n); // Declare a vector of size n

    // Read elements into the vector
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    // Call the function to find the maximum element
    int result = findMax(arr);

    // Print the result
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to find the maximum element in an array
    public static int findMax(int[] arr) {
        // Constraint N >= 1 ensures arr is not empty
        int maxVal = arr[0]; // Initialize maxVal with the first element
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > maxVal) {
                maxVal = arr[i]; // Update if a larger element is found
            }
        }
        return maxVal;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        int n = scanner.nextInt();

        // Declare an array of size n
        int[] arr = new int[n];

        // Read elements into the array
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Call the function to find the maximum element
        int result = findMax(arr);

        // Print the result
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def find_max(arr):
    """
    Function to find the maximum element in a list.
    Assumes the list is not empty based on problem constraints (N >= 1).
    """
    max_val = arr[0] # Initialize max_val with the first element
    for i in range(1, len(arr)):
        if arr[i] > max_val:
            max_val = arr[i] # Update if a larger element is found
    return max_val

if __name__ == "__main__":
    # Read the number of elements
    n = int(input())

    # Read elements into a list (assuming space-separated on one line)
    arr_str = input().split()
    arr = [int(x) for x in arr_str]

    # Call the function to find the maximum element
    result = find_max(arr)

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
let currentLine = 0;

rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    // Read the number of elements
    const n = parseInt(inputLines[currentLine++], 10);

    // Read elements into an array (assuming space-separated on the next line)
    const arr = inputLines[currentLine++].split(' ').map(Number);

    // Call the function to find the maximum element
    const result = findMax(arr);

    // Print the result
    console.log(result);
});

// Function to find the maximum element in an array
function findMax(arr) {
    // Constraint N >= 1 ensures arr is not empty
    let maxVal = arr[0]; // Initialize maxVal with the first element
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > maxVal) {
            maxVal = arr[i]; // Update if a larger element is found
        }
    }
    return maxVal;
}
```