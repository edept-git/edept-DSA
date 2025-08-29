# Solutions for The Factorial Fanfare: A Recursive Debut

### Approach
The problem asks us to compute the factorial of a non-negative integer `n` using recursion. The mathematical definition of factorial lends itself perfectly to a recursive implementation. We know that `n! = n * (n-1)!` for `n > 0`, and `0! = 1`. This gives us both our recursive step and our base case.

The algorithm is as follows:
1.  **Base Case**: If `n` is `0`, the factorial is `1`. This is the stopping condition for our recursion.
2.  **Recursive Step**: If `n` is greater than `0`, the factorial is `n` multiplied by the factorial of `n-1`. We call the same function with `n-1` as the argument, progressively reducing `n` until it hits the base case.

For example, `factorial(5)` would call `factorial(4)`, which calls `factorial(3)`, and so on, until `factorial(0)` returns `1`. Then, the results are multiplied back up the call stack: `1 * 1`, then `2 * 1`, then `3 * 2`, then `4 * 6`, and finally `5 * 24`.

**Time Complexity**: The function makes `n` recursive calls, as it decrements `n` by 1 in each step until it reaches 0. Each call involves a constant amount of work (multiplication and comparison). Therefore, the time complexity is O(n).

**Space Complexity**: Due to the recursive calls, the function's execution involves maintaining a call stack. In the worst case (for the largest `n`), there will be `n+1` stack frames (from `n` down to `0`). Each stack frame stores local variables and return addresses. Thus, the space complexity is O(n). No additional data structures beyond the call stack are used.

## C Solution
```c
#include <stdio.h>

// Function to calculate factorial recursively
long long factorial(int n) {
    // Base case: factorial of 0 is 1
    if (n == 0) {
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
    
    // Calculate factorial
    long long result = factorial(n);
    
    // Print result to stdout
    printf("%lld\n", result);
    
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate factorial recursively
long long factorial(int n) {
    // Base case: factorial of 0 is 1
    if (n == 0) {
        return 1;
    }
    // Recursive step: n! = n * (n-1)!
    return (long long)n * factorial(n - 1);
}

int main() {
    int n;
    // Read input from stdin
    std::cin >> n;
    
    // Calculate factorial
    long long result = factorial(n);
    
    // Print result to stdout
    std::cout << result << std::endl;
    
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate factorial recursively
    public static long factorial(int n) {
        // Base case: factorial of 0 is 1
        if (n == 0) {
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
        
        // Calculate factorial
        long result = factorial(n);
        
        // Print result to stdout
        System.out.println(result);
    }
}
```

## Python Solution
```python
import sys

# Function to calculate factorial recursively
def factorial(n):
    # Base case: factorial of 0 is 1
    if n == 0:
        return 1
    # Recursive step: n! = n * (n-1)!
    return n * factorial(n - 1)

if __name__ == '__main__':
    # Read input from stdin
    n = int(sys.stdin.readline().strip())
    
    # Calculate factorial
    result = factorial(n);
    
    # Print result to stdout
    sys.stdout.write(str(result) + '\n')
```

## JavaScript Solution
```javascript
// Function to calculate factorial recursively
function factorial(n) {
    // Base case: factorial of 0 is 1
    if (n === 0) {
        return 1;
    }
    // Recursive step: n! = n * (n-1)!
    return n * factorial(n - 1);
}

// Read input from stdin
// This setup assumes input is provided line by line, common in competitive programming environments.
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const n = parseInt(line.trim(), 10);
    
    // Calculate factorial
    const result = factorial(n);
    
    // Print result to stdout
    console.log(result);
    rl.close();
});
```