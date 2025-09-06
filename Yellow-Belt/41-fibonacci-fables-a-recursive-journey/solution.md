# Solutions for Fibonacci Fables: A Recursive Journey

### Approach
The most straightforward way to solve the Fibonacci sequence recursively is to directly translate its mathematical definition into code. The Fibonacci sequence is defined by two base cases and a recursive step. For the base cases, the 0th Fibonacci number is 0, and the 1st Fibonacci number is 1. For any `n > 1`, the `n`-th Fibonacci number is the sum of the `(n-1)`-th and `(n-2)`-th Fibonacci numbers. Our `fibonacci` function will first check if `n` is 0 or 1; if so, it returns `n`. Otherwise, it makes two recursive calls: `fibonacci(n - 1)` and `fibonacci(n - 2)`, and returns their sum. No special data structures are needed beyond basic integers. 

This direct recursive approach has a time complexity of O(2^n) because it re-calculates the same Fibonacci numbers multiple times (e.g., `fib(5)` calls `fib(4)` and `fib(3)`, and `fib(4)` also calls `fib(3)`, leading to redundant computations). Its space complexity is O(n) due to the depth of the recursion call stack, as each recursive call adds a frame to the stack until a base case is reached. While inefficient for larger `n`, it perfectly illustrates the concept of recursion for beginners.

## C Solution
```c
#include <stdio.h>

// Function to calculate the nth Fibonacci number recursively
int fibonacci(int n) {
    // Base cases
    if (n <= 1) {
        return n;
    }
    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;
    // Read input from stdin
    scanf("%d", &n);
    
    // Call the fibonacci function and print the result
    printf("%d\n", fibonacci(n));
    
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate the nth Fibonacci number recursively
int fibonacci(int n) {
    // Base cases
    if (n <= 1) {
        return n;
    }
    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;
    // Read input from stdin
    std::cin >> n;
    
    // Call the fibonacci function and print the result
    std::cout << fibonacci(n) << std::endl;
    
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to calculate the nth Fibonacci number recursively
    public int fibonacci(int n) {
        // Base cases
        if (n <= 1) {
            return n;
        }
        // Recursive step
        return fibonacci(n - 1) + fibonacci(n - 2);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Read input from stdin
        int n = scanner.nextInt();
        
        Main sol = new Main();
        // Call the fibonacci function and print the result
        System.out.println(sol.fibonacci(n));
        
        scanner.close();
    }
}
```

## Python Solution
```python
def fibonacci(n: int) -> int:
    """
    Calculates the nth Fibonacci number recursively.
    """
    # Base cases
    if n <= 1:
        return n
    # Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2)

if __name__ == "__main__":
    # Read input from stdin
    n = int(input())
    
    # Call the fibonacci function and print the result
    print(fibonacci(n))
```

## JavaScript Solution
```javascript
function fibonacci(n) {
    // Base cases
    if (n <= 1) {
        return n;
    }
    // Recursive step
    return fibonacci(n - 1) + fibonacci(n - 2);
}

// Read input from stdin using readline module
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const n = parseInt(line.trim(), 10);
    // Call the fibonacci function and print the result
    console.log(fibonacci(n));
    rl.close(); // Close the interface after processing the line
});
```