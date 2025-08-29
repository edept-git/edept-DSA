# Solutions for Prime Number Investigator

### Approach
To determine if a number `N` is prime, we need to check if it has any divisors other than 1 and itself.

The most straightforward approach is to iterate from `2` up to `N-1` and check if `N` is divisible by any of these numbers. If `N` is divisible by any number in this range, it's not prime. If no such divisor is found, it is prime.

However, we can optimize this. We only need to check for divisors up to the square root of `N` (`sqrt(N)`). This is because if `N` has a divisor `d` greater than `sqrt(N)`, then `N/d` must be a divisor smaller than `sqrt(N)`. So, if we haven't found a divisor up to `sqrt(N)`, we won't find one beyond it either.

Additionally, we can handle a few edge cases:
*   Numbers less than or equal to 1 are not prime.
*   The number 2 is the only even prime number.
*   For any even number greater than 2, it's not prime (as it's divisible by 2). This allows us to start checking divisibility from 3 and increment by 2 (checking only odd numbers) up to `sqrt(N)`.

**Algorithm:**
1.  If `N <= 1`, return `false`.
2.  If `N == 2`, return `true`.
3.  If `N` is even (and `N > 2`), return `false`.
4.  Loop from `i = 3` up to `sqrt(N)` (or `i * i <= N`), incrementing `i` by 2 in each step.
5.  If `N % i == 0` at any point, `N` is not prime, so return `false`.
6.  If the loop completes without finding any divisors, `N` is prime, so return `true`.

**Time Complexity:** O(sqrt(N)) because we iterate up to the square root of the input number.
**Space Complexity:** O(1) as we only use a few constant extra variables.

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>

// Function to check if a number is prime
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }
    if (n == 2) {
        return true;
    }
    if (n % 2 == 0) {
        return false;
    }
    // Check for odd divisors from 3 up to sqrt(n) using i*i <= n
    for (int i = 3; i * i <= n; i += 2) {
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

int main() {
    int num;
    // Read the input number
    scanf("%d", &num);

    // Call the isPrime function and print the result
    if (isPrime(num)) {
        printf("Yes\n");
    } else {
        printf("No\n");
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <cmath> // Not strictly needed if using i*i <= n, but good practice for sqrt concepts

// Function to check if a number is prime
bool isPrime(int n) {
    if (n <= 1) {
        return false;
    }
    if (n == 2) {
        return true;
    }
    if (n % 2 == 0) {
        return false;
    }
    // Check for odd divisors from 3 up to sqrt(n) using i*i <= n
    for (int i = 3; (long long)i * i <= n; i += 2) { // Cast to long long for i*i to prevent overflow for very large N if int is 32-bit
        if (n % i == 0) {
            return false;
        }
    }
    return true;
}

int main() {
    int num;
    // Read the input number
    std::cin >> num;

    // Call the isPrime function and print the result
    if (isPrime(num)) {
        std::cout << "Yes" << std::endl;
    } else {
        std::cout << "No" << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class PrimeChecker {

    // Function to check if a number is prime
    public static boolean isPrime(int n) {
        if (n <= 1) {
            return false;
        }
        if (n == 2) {
            return true;
        }
        if (n % 2 == 0) {
            return false;
        }
        // Check for odd divisors from 3 up to sqrt(n) using (long)i * i <= n
        for (int i = 3; (long)i * i <= n; i += 2) {
            if (n % i == 0) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt(); // Read the input number
        scanner.close();

        // Call the isPrime function and print the result
        if (isPrime(num)) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
    }
}
```

## Python Solution
```python
import math

# Function to check if a number is prime
def is_prime(n):
    if n <= 1:
        return False
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    
    # Check for odd divisors from 3 up to sqrt(n)
    # math.isqrt can be used for integer square root in Python 3.8+
    # For compatibility, using int(math.sqrt(n)) + 1 for the range limit.
    limit = int(math.sqrt(n)) + 1 
    for i in range(3, limit, 2):
        if n % i == 0:
            return False
    return True

def main():
    num = int(input()) # Read the input number

    # Call the is_prime function and print the result
    if is_prime(num):
        print("Yes")
    else:
        print("No")

if __name__ == "__main__":
    main()
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
    if (n % 2 === 0) {
        return false;
    }
    
    // Check for odd divisors from 3 up to sqrt(n) using i*i <= n
    for (let i = 3; i * i <= n; i += 2) {
        if (n % i === 0) {
            return false;
        }
    }
    return true;
}

// Node.js specific: Read input from stdin
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const num = parseInt(line); // Convert input string to integer
    
    // Call the isPrime function and print the result
    if (isPrime(num)) {
        console.log("Yes");
    } else {
        console.log("No");
    }
    rl.close(); // Close the readline interface after processing one line
});
```