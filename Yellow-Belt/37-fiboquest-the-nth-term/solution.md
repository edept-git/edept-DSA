# Solutions for FiboQuest: The Nth Term

### Approach
The problem asks for the Nth Fibonacci number using a recursive approach. The Fibonacci sequence is defined by the recurrence relation `F(n) = F(n-1) + F(n-2)`. To implement this recursively, we need to define the base cases. The standard base cases for the Fibonacci sequence are `F(0) = 0` and `F(1) = 1`.

The algorithm proceeds as follows:
1. If `n` is 0, return 0 (base case).
2. If `n` is 1, return 1 (base case).
3. Otherwise, recursively call the function for `n-1` and `n-2`, and return their sum: `fibonacci(n-1) + fibonacci(n-2)`.

This approach directly translates the mathematical definition of the Fibonacci sequence into code. Each recursive call adds a new frame to the call stack until a base case is reached. After the base cases return their values, the results propagate back up the call stack, summing at each level, until the initial call returns the final Nth Fibonacci number.

**Time Complexity:** The time complexity of this naive recursive solution is exponential, specifically O(2^n). This is because the same subproblems (e.g., `fibonacci(3)`) are computed multiple times within the recursion tree. For example, to compute `fibonacci(5)`, `fibonacci(3)` is computed as part of `fibonacci(4)` and again as part of `fibonacci(5)`.

**Space Complexity:** The space complexity is O(n). This is due to the depth of the recursion stack. In the worst case, the stack depth will be proportional to `n` as the function calls itself until it reaches the base cases `n=0` or `n=1`.

## C Solution
```c
#include <stdio.h>

// Function to calculate the Nth Fibonacci number recursively
int fibonacci(int n) {
    // Base cases
    if (n == 0) {
        return 0;
    }
    if (n == 1) {
        return 1;
    }
    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;

    // Read input from stdin
    if (scanf("%d", &n) != 1) {
        // Handle error if input is not a valid integer
        return 1;
    }

    // Calculate and print the Nth Fibonacci number
    int result = fibonacci(n);
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate the Nth Fibonacci number recursively
int fibonacci(int n) {
    // Base cases
    if (n == 0) {
        return 0;
    }
    if (n == 1) {
        return 1;
    }
    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;

    // Read input from stdin
    std::cin >> n;

    // Calculate and print the Nth Fibonacci number
    int result = fibonacci(n);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate the Nth Fibonacci number recursively
    public int fibonacci(int n) {
        // Base cases
        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        // Recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Read input from stdin
        int n = scanner.nextInt();
        
        // Create an instance of the Solution class to call the non-static method
        Solution sol = new Solution();
        
        // Calculate and print the Nth Fibonacci number
        int result = sol.fibonacci(n);
        System.out.println(result);
        
        scanner.close();
    }
}
```

## Python Solution
```python
def fibonacci(n: int) -> int:
    """
    Calculates the Nth Fibonacci number recursively.
    """
    # Base cases
    if n == 0:
        return 0
    if n == 1:
        return 1
    # Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2)

if __name__ == "__main__":
    # Read input from stdin
    n = int(input())
    
    # Calculate and print the Nth Fibonacci number
    result = fibonacci(n)
    print(result)

```

## JavaScript Solution
```javascript
// Function to calculate the Nth Fibonacci number recursively
function fibonacci(n) {
    // Base cases
    if (n === 0) {
        return 0;
    }
    if (n === 1) {
        return 1;
    }
    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// Read input from stdin and print output to stdout
// This setup is common for competitive programming environments in Node.js
process.stdin.resume();
process.stdin.setEncoding('utf8');

let inputString = '';
let currentLine = 0;

process.stdin.on('data', chunk => {
    inputString += chunk;
});

process.stdin.on('end', _ => {
    inputString = inputString.trim().split('\n').map(str => str.trim());
    main();
});

function readLine() {
    return inputString[currentLine++];
}

function main() {
    const n = parseInt(readLine(), 10);
    
    const result = fibonacci(n);
    console.log(result);
}
```