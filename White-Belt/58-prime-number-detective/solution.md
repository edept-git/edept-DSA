# Solutions for Prime Number Detective

### Approach
To determine if a number `N` is prime, we can follow these steps:
1.  **Handle Edge Cases:**
    *   If `N` is less than or equal to 1, it is not prime. Return `false`.
    *   If `N` is 2, it is prime. Return `true`. (2 is the only even prime number).
2.  **Optimize for Even Numbers:**
    *   If `N` is an even number greater than 2, it is divisible by 2, and therefore not prime. Return `false`.
3.  **Check for Odd Divisors:**
    *   For any odd number `N` greater than 2, we need to check if it has any divisors other than 1 and itself.
    *   We can iterate through odd numbers starting from 3 up to the square root of `N`. Why the square root? If `N` has a divisor `d` greater than `sqrt(N)`, then it must also have a divisor `N/d` which is less than `sqrt(N)`. So, we only need to check for divisors up to `sqrt(N)`. We can implement `i <= sqrt(N)` as `i * i <= N` to avoid floating-point calculations.
    *   In each iteration, if we find any odd number `i` that divides `N` evenly (i.e., `N % i == 0`), then `N` is not prime. Return `false`.
4.  **No Divisors Found:**
    *   If the loop completes without finding any divisors, then `N` has no divisors other than 1 and itself (and we've already handled 2), meaning it is prime. Return `true`.

**Data Structures:**
No complex data structures are required; we only work with the input integer `N`.

**Time Complexity:**
The time complexity is **O(sqrt(N))** because in the worst case, we iterate from 3 up to the square root of `N`, checking only odd numbers.

**Space Complexity:**
The space complexity is **O(1)** as we only use a few constant variables to store the input and loop counter, regardless of the size of `N`.

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>
#include <math.h> // For sqrt (though i*i <= n avoids direct usage, it's good practice for concept)

// Function to check if a number is prime
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }
    if (n == 2) {
        return true;
    }
    // Optimization: even numbers greater than 2 are not prime
    if (n % 2 == 0) {
        return false;
    }
    // Check for odd divisors from 3 up to sqrt(n)
    // i*i <= n is used instead of i <= sqrt(n) to avoid float operations and potential precision issues.
    for (int i = 3; i * i <= n; i += 2) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

int main() {
    int n;
    // Read input from stdin
    if (scanf("%d", &n) != 1) {
        return 1; // Error reading input
    }

    // Call the isPrime function and print the result
    if (isPrime(n)) {
        printf("true\n");
    } else {
        printf("false\n");
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <cmath> // For sqrt (though i*i <= n avoids direct usage, it's good practice for concept)

// Function to check if a number is prime
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }
    if (n == 2) {
        return true;
    }
    // Optimization: even numbers greater than 2 are not prime
    if (n % 2 == 0) {
        return false;
    }
    // Check for odd divisors from 3 up to sqrt(n)
    // i*i <= n is used instead of i <= sqrt(n) to avoid float operations and potential precision issues.
    for (int i = 3; i * i <= n; i += 2) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

int main() {
    int n;
    // Read input from stdin
    std::cin >> n;

    // Call the isPrime function and print the result
    if (isPrime(n)) {
        std::cout << "true" << std::endl;
    } else {
        std::cout << "false" << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.lang.Math; // For Math.sqrt (though i*i <= n avoids direct usage, it's good practice for concept)

public class Solution {

    // Function to check if a number is prime
    public static boolean isPrime(int n) {
        if (n <= 1) {
            return false;
        }
        if (n == 2) {
            return true;
        }
        // Optimization: even numbers greater than 2 are not prime
        if (n % 2 == 0) {
            return false;
        }
        // Check for odd divisors from 3 up to sqrt(n)
        // i*i <= n is used instead of i <= Math.sqrt(n) to avoid float operations and potential precision issues.
        for (int i = 3; i * i <= n; i += 2) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Read input from stdin
        int n = scanner.nextInt();
        scanner.close();

        // Call the isPrime function and print the result
        if (isPrime(n)) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
    }
}
```

## Python Solution
```python
import math

# Function to check if a number is prime
def isPrime(n: int) -> bool:
    if n <= 1:
        return False
    if n == 2:
        return True
    # Optimization: even numbers greater than 2 are not prime
    if n % 2 == 0:
        return False
    # Check for odd divisors from 3 up to sqrt(n)
    # The loop condition for i * i <= n is equivalent to i <= math.sqrt(n)
    # and avoids floating point issues/conversions while keeping it integer arithmetic.
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        if n % i == 0:
            return False
    return True

# Read input from stdin
n = int(input())

# Call the isPrime function and print the result
if isPrime(n):
    print("true")
else:
    print("false")
```

## JavaScript Solution
```javascript
// Function to check if a number is prime
function isPrime(n) {
    if (n <= 1) {
        return false;
    }
    if (n === 2) {
        return true;
    }
    // Optimization: even numbers greater than 2 are not prime
    if (n % 2 === 0) {
        return false;
    }
    // Check for odd divisors from 3 up to sqrt(n)
    // i*i <= n is used instead of i <= Math.sqrt(n) to avoid float operations and potential precision issues.
    for (let i = 3; i * i <= n; i += 2) {
        if (n % i === 0) {
            return false;
        }
    }
    return true;
}

// Read input from stdin
// This setup is common for competitive programming environments that use Node.js
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let input = '';
rl.on('line', (line) => {
    input += line;
});

rl.on('close', () => {
    const n = parseInt(input.trim(), 10);
    // Call the isPrime function and print the result
    if (isPrime(n)) {
        console.log("true");
    } else {
        console.log("false");
    }
});
```