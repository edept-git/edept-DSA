# Solutions for Recursive Rungs: Factorial Fun

### Approach
This problem is a classic introduction to recursion. The factorial function can be defined recursively as follows: `n! = n * (n-1)!` for `n > 1`, and `0! = 1`. A common variation is `1! = 1`, which can be combined with `0! = 1` to form a single base case. Therefore, our recursive function will have a base case where if `n` is `0` or `1`, it returns `1`. For any `n > 1`, the function will return `n` multiplied by the result of calling itself with `n - 1`. No special data structures are required, as we are simply performing arithmetic operations. The time complexity of this recursive solution is O(n), because the function makes `n` recursive calls. The space complexity is also O(n), due to the call stack depth that grows linearly with `n`.

## C Solution
```c
#include <stdio.h>

// Function to calculate factorial recursively
long long factorial(int n) {
    // Base case: 0! and 1! are both 1
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
    // Calculate factorial and print to stdout
    long long result = factorial(n);
    printf("%lld\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate factorial recursively
long long factorial(int n) {
    // Base case: 0! and 1! are both 1
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
    // Calculate factorial and print to stdout
    long long result = factorial(n);
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
        // Base case: 0! and 1! are both 1
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
        // Calculate factorial and print to stdout
        long result = factorial(n);
        System.out.println(result);
        scanner.close();
    }
}
```

## Python Solution
```python
import sys

# Function to calculate factorial recursively
def factorial(n):
    # Base case: 0! and 1! are both 1
    if n == 0 or n == 1:
        return 1
    # Recursive step: n! = n * (n-1)!
    return n * factorial(n - 1)

def main():
    # Read input from stdin
    n = int(sys.stdin.readline())
    # Calculate factorial and print to stdout
    result = factorial(n)
    sys.stdout.write(str(result) + "\n")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Function to calculate factorial recursively
function factorial(n) {
    // Base case: 0! and 1! are both 1
    if (n === 0 || n === 1) {
        return 1;
    }
    // Recursive step: n! = n * (n-1)!
    return n * factorial(n - 1);
}

// Main function to handle input/output
function main() {
    // Read input from stdin
    const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim();
    const n = parseInt(input, 10);

    // Calculate factorial and print to stdout
    const result = factorial(n);
    console.log(result);
}

main();
```