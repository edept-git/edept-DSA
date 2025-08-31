# Solutions for The Factorial Fanfare: A Recursive Debut

### Approach
To calculate the factorial of `n` recursively, we need to identify a base case and a recursive step. The base case occurs when `n` is small enough that its factorial can be computed directly without further recursion. For factorials, `0!` is defined as `1`, and `1!` is also `1`. Thus, if `n` is `0` or `1`, the function should return `1`. This serves as our base case, preventing infinite recursion. The recursive step is based on the mathematical definition: `n! = n * (n-1)!`. So, for `n > 1`, we can return `n` multiplied by the result of calling the factorial function with `n-1`. This breaks down the problem into smaller, identical subproblems until the base case is reached. The function will use primitive integer types for its calculations.

The time complexity of this approach is O(n) because for an input `n`, the function will make `n` recursive calls (e.g., `factorial(n)`, `factorial(n-1)`, ..., `factorial(1)`). Each call involves a constant amount of work. The space complexity is also O(n) due to the recursive call stack. Each time `factorial` is called, a new stack frame is added, and these frames accumulate until the base case is hit and they start unwinding. The maximum depth of the stack will be `n`.

## C Solution
```c
#include <stdio.h>

// Function to calculate factorial recursively
long long factorial(int n) {
    // Base case: 0! = 1, 1! = 1
    if (n == 0 || n == 1) {
        return 1;
    }
    // Recursive step: n! = n * (n-1)!
    return (long long)n * factorial(n - 1);
}

int main() {
    int n;
    // Read input from stdin
    if (scanf("%d", &n) != 1) {
        return 1; // Error reading input
    }

    // Call the factorial function and print the result to stdout
    printf("%lld\n", factorial(n));

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate factorial recursively
long long factorial(int n) {
    // Base case: 0! = 1, 1! = 1
    if (n == 0 || n == 1) {
        return 1;
    }
    // Recursive step: n! = n * (n-1)!
    return (long long)n * factorial(n - 1);
}

int main() {
    int n;
    // Read input from stdin
    std::cin >> n;

    // Call the factorial function and print the result to stdout
    std::cout << factorial(n) << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {

    // Function to calculate factorial recursively
    public static long factorial(int n) {
        // Base case: 0! = 1, 1! = 1
        if (n == 0 || n == 1) {
            return 1;
        }
        // Recursive step: n! = n * (n-1)!
        return (long)n * factorial(n - 1);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Read input from stdin
        int n = scanner.nextInt();
        scanner.close();

        // Call the factorial function and print the result to stdout
        System.out.println(factorial(n));
    }
}
```

## Python Solution
```python
# Function to calculate factorial recursively
def factorial(n):
    # Base case: 0! = 1, 1! = 1
    if n == 0 or n == 1:
        return 1
    # Recursive step: n! = n * (n-1)!
    return n * factorial(n - 1)

if __name__ == '__main__':
    # Read input from stdin
    n = int(input())

    # Call the factorial function and print the result to stdout
    print(factorial(n))
```

## JavaScript Solution
```javascript
// Function to calculate factorial recursively
function factorial(n) {
    // Base case: 0! = 1, 1! = 1
    if (n === 0 || n === 1) {
        return 1;
    }
    // Recursive step: n! = n * (n-1)!
    return n * factorial(n - 1);
}

// Read input from stdin
// For competitive programming environments, input usually comes from /dev/stdin
// or equivalent. For local testing, you might pass a string directly.
const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim();
const n = parseInt(input, 10);

// Call the factorial function and print the result to stdout
console.log(factorial(n));
```