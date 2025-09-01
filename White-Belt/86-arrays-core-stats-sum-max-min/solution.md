# Solutions for Array's Core Stats: Sum, Max, Min

### Approach
The most straightforward and efficient way to solve this problem is to iterate through the array exactly once. We can initialize three variables: `sum` to 0, `max_val` to a very small number (or the first element of the array), and `min_val` to a very large number (or the first element of the array). As we traverse each element of the array:
1.  Add the current element to `sum`.
2.  Compare the current element with `max_val`; if the current element is greater, update `max_val`.
3.  Compare the current element with `min_val`; if the current element is smaller, update `min_val`.

After iterating through all elements, `sum`, `max_val`, and `min_val` will hold the correct results. This approach ensures that each element is processed exactly once. Therefore, the time complexity will be O(N), where N is the number of elements in the array. The space complexity is O(1) because we only use a few constant-size variables regardless of the input array's size.

## C Solution
```c
#include <stdio.h>
#include <limits.h> // For INT_MIN and INT_MAX

// Function to analyze the array for sum, max, and min
void analyzeArray(int arr[], int n, int* sum_val, int* max_val, int* min_val) {
    if (n == 0) {
        *sum_val = 0;
        *max_val = 0; // Or some error indicator, as per problem constraints, n >= 1
        *min_val = 0;
        return;
    }

    *sum_val = 0;
    *max_val = INT_MIN; // Initialize with smallest possible integer value
    *min_val = INT_MAX; // Initialize with largest possible integer value

    for (int i = 0; i < n; i++) {
        *sum_val += arr[i];
        if (arr[i] > *max_val) {
            *max_val = arr[i];
        }
        if (arr[i] < *min_val) {
            *min_val = arr[i];
        }
    }
}

int main() {
    int n;
    // Read the number of elements
    if (scanf("%d", &n) != 1 || n <= 0) {
        return 1; // Error reading N or N is invalid
    }

    int arr[n]; // C99 VLA - Variable Length Array

    // Read the array elements
    for (int i = 0; i < n; i++) {
        if (scanf("%d", &arr[i]) != 1) {
            return 1; // Error reading array element
        }
    }

    int sum_result, max_result, min_result;

    // Call the analysis function
    analyzeArray(arr, n, &sum_result, &max_result, &min_result);

    // Print the results
    printf("Sum: %d, Max: %d, Min: %d\n", sum_result, max_result, min_result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::max and std::min, or just manual comparison
#include <limits>    // For std::numeric_limits

// Function to analyze the array for sum, max, and min
void analyzeArray(const std::vector<int>& arr, int& sum_val, int& max_val, int& min_val) {
    if (arr.empty()) {
        sum_val = 0;
        max_val = 0; // Or handle as an error, per problem, arr not empty
        min_val = 0;
        return;
    }

    sum_val = 0;
    max_val = std::numeric_limits<int>::min(); // Initialize with smallest possible int value
    min_val = std::numeric_limits<int>::max(); // Initialize with largest possible int value

    for (int x : arr) {
        sum_val += x;
        max_val = std::max(max_val, x);
        min_val = std::min(min_val, x);
    }
}

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

    int sum_result, max_result, min_result;

    // Call the analysis function
    analyzeArray(arr, sum_result, max_result, min_result);

    // Print the results
    std::cout << "Sum: " << sum_result << ", Max: " << max_result << ", Min: " << min_result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {

    // Function to analyze the array for sum, max, and min
    // Returns an array: [sum, max, min]
    public int[] analyzeArray(int[] arr) {
        if (arr == null || arr.length == 0) {
            return new int[]{0, 0, 0}; // Should not happen based on constraints
        }

        int sum = 0;
        int maxVal = Integer.MIN_VALUE;
        int minVal = Integer.MAX_VALUE;

        for (int x : arr) {
            sum += x;
            if (x > maxVal) {
                maxVal = x;
            }
            if (x < minVal) {
                minVal = x;
            }
        }
        return new int[]{sum, maxVal, minVal};
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

        Solution sol = new Solution();
        int[] results = sol.analyzeArray(arr);

        // Print the results
        System.out.println("Sum: " + results[0] + ", Max: " + results[1] + ", Min: " + results[2]);

        scanner.close();
    }
}
```

## Python Solution
```python
def analyze_array(arr):
    """
    Analyzes an array to find its sum, maximum, and minimum values.
    Args:
        arr (list[int]): The input list of integers.
    Returns:
        tuple[int, int, int]: A tuple containing (sum, max_val, min_val).
    """
    if not arr:
        return 0, 0, 0 # According to constraints, arr will not be empty

    total_sum = 0
    max_val = arr[0] # Initialize with the first element
    min_val = arr[0] # Initialize with the first element

    for x in arr:
        total_sum += x
        if x > max_val:
            max_val = x
        if x < min_val:
            min_val = x
            
    return total_sum, max_val, min_val

if __name__ == "__main__":
    # Read the number of elements
    n = int(input())

    # Read the array elements
    # Using map(int, input().split()) to parse space-separated integers
    arr_str = input().split()
    arr = [int(x) for x in arr_str]

    # Call the analysis function
    sum_result, max_result, min_result = analyze_array(arr)

    # Print the results
    print(f"Sum: {sum_result}, Max: {max_result}, Min: {min_result}")
```

## JavaScript Solution
```javascript
function analyzeArray(arr) {
    if (!arr || arr.length === 0) {
        return [0, 0, 0]; // Should not happen based on constraints
    }

    let sum = 0;
    let maxVal = Number.MIN_SAFE_INTEGER; // Initialize with smallest possible integer value
    let minVal = Number.MAX_SAFE_INTEGER; // Initialize with largest possible integer value

    for (let i = 0; i < arr.length; i++) {
        const x = arr[i];
        sum += x;
        if (x > maxVal) {
            maxVal = x;
        }
        if (x < minVal) {
            minVal = x;
        }
    }
    return [sum, maxVal, minVal];
}

// Handle input/output for Node.js environment
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
    // The first line is 'n', the number of elements (though not strictly needed after reading array)
    // const n = parseInt(inputLines[0], 10);
    
    // The second line contains the array elements as space-separated string
    const arr = inputLines[1].split(' ').map(Number);

    // Call the analysis function
    const [sumResult, maxResult, minResult] = analyzeArray(arr);

    // Print the results
    console.log(`Sum: ${sumResult}, Max: ${maxResult}, Min: ${minResult}`);
});
```