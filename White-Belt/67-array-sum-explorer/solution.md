# Solutions for Array Sum Explorer

### Approach
To calculate the sum of all elements in an array, the most straightforward approach is to iterate through each element of the array exactly once. We can initialize a variable, let's call it `totalSum`, to zero. Then, as we traverse the array from the first element to the last, we add each element's value to `totalSum`. After visiting every element, `totalSum` will hold the complete sum of the array. This algorithm requires a simple loop. 

In terms of data structures, we only use the input array itself and a single integer variable to store the running sum. No additional complex data structures are needed.

**Time Complexity:** The algorithm visits each of the `N` elements in the array exactly once to add it to the sum. Therefore, the time taken grows linearly with the number of elements in the array. This is expressed as **O(N)**, where N is the number of elements in the array.

**Space Complexity:** We only use a few constant variables (like a loop counter and the `totalSum` variable) regardless of how large the input array is. The amount of memory used does not depend on the input size `N`. This is expressed as **O(1)**, meaning constant space.

## C Solution
```c
#include <stdio.h>

// Function to calculate the sum of array elements
long long calculateArraySum(int arr[], int n) {
    long long sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    int n;
    // Read the number of elements
    scanf("%d", &n);

    int arr[n]; // Declare array of size n (VLA - C99 feature)
    // Read the elements into the array
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    // Calculate the sum using the helper function
    long long result = calculateArraySum(arr, n);

    // Print the result
    printf("%lld\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric> // For std::accumulate, though we'll implement manually for learning

// Function to calculate the sum of array elements
long long calculateArraySum(const std::vector<int>& arr) {
    long long sum = 0;
    for (int x : arr) {
        sum += x;
    }
    return sum;
    // Alternatively, using standard library for brevity (but less illustrative for beginners):
    // return std::accumulate(arr.begin(), arr.end(), 0LL);
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    // Read the number of elements
    std::cin >> n;

    std::vector<int> arr(n);
    // Read the elements into the vector
    for (int i = 0; i < n; i++) {
        std::cin >> arr[i];
    }

    // Calculate the sum using the helper function
    long long result = calculateArraySum(arr);

    // Print the result
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate the sum of array elements
    public static long calculateArraySum(int[] arr) {
        long sum = 0;
        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
        }
        return sum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        int n = scanner.nextInt();

        int[] arr = new int[n];
        // Read the elements into the array
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Calculate the sum using the helper function
        long result = calculateArraySum(arr);

        // Print the result
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def calculate_array_sum(arr):
    # Function to calculate the sum of array elements
    total_sum = 0
    for x in arr:
        total_sum += x
    return total_sum

if __name__ == '__main__':
    # Read the number of elements
    n = int(input())

    # Read the elements into a list
    # Using map(int, input().split()) is a common Pythonic way to read space-separated integers
    arr = list(map(int, input().split()))

    # Calculate the sum using the helper function
    result = calculate_array_sum(arr)

    # Print the result
    print(result)
```

## JavaScript Solution
```javascript
function calculateArraySum(arr) {
    // Function to calculate the sum of array elements
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}

// Main part to handle input and output
function main() {
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
        // The first line is n, the number of elements (not strictly needed for JS array length)
        // const n = parseInt(inputLines[0]); 
        
        // The second line contains space-separated integers
        const arr = inputLines[1].split(' ').map(Number);

        // Calculate the sum using the helper function
        const result = calculateArraySum(arr);

        // Print the result
        console.log(result);
    });
}

main();
```