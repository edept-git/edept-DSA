# Solutions for Number's Best Friends: GCD and LCM

### Approach
The problem asks us to find both the Greatest Common Divisor (GCD) and the Least Common Multiple (LCM) of two given positive integers, `a` and `b`.

To find the GCD, the most efficient and widely used method is the Euclidean Algorithm. This algorithm is based on the principle that the GCD of two numbers does not change if the larger number is replaced by its difference with the smaller number. This process is repeated until one of the numbers becomes zero, at which point the other number is the GCD. More formally, `GCD(a, b) = GCD(b, a % b)` if `b` is not zero, and `GCD(a, 0) = a`. This can be implemented iteratively or recursively.

Once the GCD of `a` and `b` is found, the LCM can be easily calculated using the fundamental relationship between GCD and LCM: `LCM(a, b) = (a * b) / GCD(a, b)`. It's important to perform the multiplication `a * b` using a data type that can accommodate large products (like `long long` in C++/C or `long` in Java), as `a` and `b` can be up to `10^5`, making their product up to `10^10`, which exceeds the capacity of a standard 32-bit integer. To prevent potential overflow even before division, a common safe practice is `LCM(a, b) = (a / GCD(a, b)) * b`.

**Algorithm Steps:**
1.  Implement a helper function `findGCD(num1, num2)` using the iterative Euclidean Algorithm.
2.  In the main logic function, call `findGCD(a, b)` to get the GCD value.
3.  Calculate LCM using the formula: `LCM = (a / GCD) * b`. This ensures that intermediate products remain within representable limits if `a * b` itself would overflow, while also guaranteeing integer division because `a` is divisible by `GCD(a,b)`.
4.  Return both GCD and LCM.

**Time Complexity:** The Euclidean algorithm takes logarithmic time, specifically O(log(min(a, b))). Calculating LCM is a constant time operation after GCD is found. Thus, the overall time complexity is O(log(min(a, b))).
**Space Complexity:** O(1) for the iterative Euclidean algorithm, as it only uses a few variables regardless of input size. The recursive version would use O(log(min(a, b))) stack space.

## C Solution
```c
#include <stdio.h>

// Function to calculate GCD using Euclidean algorithm
long long findGCD(long long a, long long b) {
    while (b != 0) {
        long long temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to calculate GCD and LCM
// Returns GCD in result[0] and LCM in result[1]
void calculateGcdAndLcm(long long a, long long b, long long result[]) {
    long long gcd_val = findGCD(a, b);
    // Calculate LCM using the formula: LCM(a, b) = (a * b) / GCD(a, b)
    // Use (a / gcd_val) * b to prevent potential overflow if (a * b) exceeds long long max before division
    long long lcm_val = (a / gcd_val) * b;
    result[0] = gcd_val;
    result[1] = lcm_val;
}

int main() {
    long long a, b;
    // Read two long long integers from stdin
    if (scanf("%lld %lld", &a, &b) != 2) {
        // Handle error if input is not as expected
        return 1;
    }

    long long results[2]; // Array to store GCD and LCM
    calculateGcdAndLcm(a, b, results);

    // Print the results to stdout
    printf("GCD: %lld\n", results[0]);
    printf("LCM: %lld\n", results[1]);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <utility> // For std::pair

// Function to calculate GCD using Euclidean algorithm
long long findGCD(long long a, long long b) {
    while (b != 0) {
        long long temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to calculate GCD and LCM
// Returns a std::pair where first is GCD and second is LCM
std::pair<long long, long long> calculateGcdAndLcm(long long a, long long b) {
    long long gcd_val = findGCD(a, b);
    // Calculate LCM using the formula: LCM(a, b) = (a * b) / GCD(a, b)
    // Use (a / gcd_val) * b to prevent potential overflow if (a * b) exceeds long long max before division
    long long lcm_val = (a / gcd_val) * b;
    return {gcd_val, lcm_val};
}

int main() {
    // Optimize C++ standard streams for faster input/output
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    long long a, b;
    // Read two long long integers from stdin
    if (!(std::cin >> a >> b)) {
        // Handle error if input is not as expected
        return 1;
    }

    // Call the logic function to get GCD and LCM
    std::pair<long long, long long> results = calculateGcdAndLcm(a, b);

    // Print the results to stdout
    std::cout << "GCD: " << results.first << "\n";
    std::cout << "LCM: " << results.second << "\n";

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class GcdLcmCalculator {

    // Function to calculate GCD using Euclidean algorithm
    public static long findGCD(long a, long b) {
        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    // Function to calculate GCD and LCM
    // Returns an array where result[0] is GCD and result[1] is LCM
    public static long[] calculateGcdAndLcm(long a, long b) {
        long gcd_val = findGCD(a, b);
        // Calculate LCM using the formula: LCM(a, b) = (a * b) / GCD(a, b)
        // Use (a / gcd_val) * b to prevent potential overflow if (a * b) exceeds long max before division
        long lcm_val = (a / gcd_val) * b;
        return new long[]{gcd_val, lcm_val};
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read two long integers from stdin
        if (!scanner.hasNextLong()) {
            System.err.println("Invalid input. Please enter two long integers.");
            return;
        }
        long a = scanner.nextLong();

        if (!scanner.hasNextLong()) {
            System.err.println("Invalid input. Please enter two long integers.");
            return;
        }
        long b = scanner.nextLong();

        scanner.close();

        // Call the logic function to get GCD and LCM
        long[] results = calculateGcdAndLcm(a, b);

        // Print the results to stdout
        System.out.println("GCD: " + results[0]);
        System.out.println("LCM: " + results[1]);
    }
}
```

## Python Solution
```python
import sys

def find_gcd(a, b):
    """Function to calculate GCD using Euclidean algorithm."""
    while b:
        a, b = b, a % b
    return a

def calculate_gcd_and_lcm(a, b):
    """Function to calculate GCD and LCM."""
    gcd_val = find_gcd(a, b)
    # Python integers handle arbitrary size, so (a * b) // gcd_val is safe from overflow.
    lcm_val = (a * b) // gcd_val
    return gcd_val, lcm_val

def main():
    """Main function to handle input/output and call the logic."""
    # Read two integers from stdin
    input_line = sys.stdin.readline().strip().split()
    a = int(input_line[0])
    b = int(input_line[1])

    # Call the logic function to get GCD and LCM
    gcd_val, lcm_val = calculate_gcd_and_lcm(a, b)

    # Print the results to stdout
    sys.stdout.write(f"GCD: {gcd_val}\n")
    sys.stdout.write(f"LCM: {lcm_val}\n")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
function findGcd(a, b) {
    """Function to calculate GCD using Euclidean algorithm."""
    while (b !== 0) {
        let temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

function calculateGcdAndLcm(a, b) {
    """Function to calculate GCD and LCM."""
    const gcdVal = findGcd(a, b);
    // JavaScript numbers are 64-bit floating point, providing enough precision for a*b up to 10^10.
    // (a / gcdVal) * b is used to mirror the logic in other languages for consistency and safety.
    const lcmVal = (a / gcdVal) * b;
    return { gcd: gcdVal, lcm: lcmVal };
}

function main() {
    """Main function to handle input/output and call the logic."""
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    rl.on('line', (line) => {
        const [a, b] = line.split(' ').map(Number);
        
        // Call the logic function to get GCD and LCM
        const results = calculateGcdAndLcm(a, b);
        
        // Print the results to stdout
        console.log(`GCD: ${results.gcd}`);
        console.log(`LCM: ${results.lcm}`);
        rl.close(); // Close the readline interface after processing one line
    });
}

main();
```