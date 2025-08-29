# Solutions for Casting Call: Integer and Double Duet

### Approach
The problem primarily focuses on demonstrating type casting between integers and floating-point numbers. To convert an integer to a double, most programming languages implicitly handle this during assignment or arithmetic operations, but an explicit cast (e.g., `(double)A`) can be used for clarity. When converting a double to an integer, an explicit cast (e.g., `(int)B`) is generally required to truncate the decimal part, as implicit conversion might not be available or may behave differently. After these conversions, standard addition operations are performed. The time complexity for this problem is O(1) because it involves a fixed number of operations regardless of the input values. The space complexity is also O(1) as only a few variables are used to store the input and calculated results.

## C Solution
```c
#include <stdio.h>

void performTypeCasting(int a, double b) {
    // 1. Convert integer A to a double
    double double_A = (double)a;

    // 2. Convert double B to an integer (truncating decimal part)
    int int_B = (int)b;

    // 3. Calculate sum of double_A and original double B
    double double_sum = double_A + b;

    // 4. Calculate sum of original integer A and int_B
    int int_sum = a + int_B;

    // Print results
    printf("%.2f\n", double_A);
    printf("%d\n", int_B);
    printf("%.2f\n", double_sum);
    printf("%d\n", int_sum);
}

int main() {
    int a;
    double b;
    // Read input
    if (scanf("%d %lf", &a, &b) != 2) {
        return 1; // Indicate an error if input reading fails
    }
    // Call the core logic function
    performTypeCasting(a, b);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <iomanip> // Required for std::fixed and std::setprecision

void performTypeCasting(int a, double b) {
    // 1. Convert integer A to a double using static_cast for explicit conversion
    double double_A = static_cast<double>(a);

    // 2. Convert double B to an integer, truncating decimal part using static_cast
    int int_B = static_cast<int>(b);

    // 3. Calculate sum of double_A and original double B
    double double_sum = double_A + b;

    // 4. Calculate sum of original integer A and int_B
    int int_sum = a + int_B;

    // Print results with specified formatting
    std::cout << std::fixed << std::setprecision(2) << double_A << std::endl;
    std::cout << int_B << std::endl;
    std::cout << std::fixed << std::setprecision(2) << double_sum << std::endl;
    std::cout << int_sum << std::endl;
}

int main() {
    int a;
    double b;
    // Read input
    if (!(std::cin >> a >> b)) {
        return 1; // Indicate an error if input reading fails
    }
    // Call the core logic function
    performTypeCasting(a, b);
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    public static void performTypeCasting(int a, double b) {
        // 1. Convert integer A to a double
        double double_A = (double) a; // Explicit cast for clarity

        // 2. Convert double B to an integer, truncating decimal part
        int int_B = (int) b;          // Explicit cast

        // 3. Calculate sum of double_A and original double B
        double double_sum = double_A + b;

        // 4. Calculate sum of original integer A and int_B
        int int_sum = a + int_B;

        // Print results with specified formatting
        System.out.printf("%.2f%n", double_A); // %.2f for two decimal places, %n for new line
        System.out.println(int_B);
        System.out.printf("%.2f%n", double_sum);
        System.out.println(int_sum);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        try {
            // Read input
            int a = scanner.nextInt();
            double b = scanner.nextDouble();
            // Call the core logic function
            performTypeCasting(a, b);
        } finally {
            scanner.close(); // Close the scanner to prevent resource leaks
        }
    }
}
```

## Python Solution
```python
def performTypeCasting(a, b):
    # 1. Convert integer A to a float (Python's equivalent of double)
    double_A = float(a) # Explicit cast

    # 2. Convert float B to an integer, truncating decimal part
    int_B = int(b)      # Explicit cast (truncates)

    # 3. Calculate sum of double_A and original float B
    double_sum = double_A + b

    # 4. Calculate sum of original integer A and int_B
    int_sum = a + int_B

    # Print results with specified formatting
    print(f"{double_A:.2f}") # f-string for formatted output
    print(int_B)
    print(f"{double_sum:.2f}")
    print(int_sum)

if __name__ == "__main__":
    # Read input from stdin
    line = input().split()
    a = int(line[0])
    b = float(line[1])
    # Call the core logic function
    performTypeCasting(a, b)

```

## JavaScript Solution
```javascript
function performTypeCasting(a, b) {
    // In JavaScript, all numbers are 64-bit floating-point. 
    // So, 'a' is conceptually already a double. We use parseFloat for clarity of intent.
    // 1. Treat integer 'a' as a double
    let double_A = parseFloat(a);

    // 2. Convert double 'b' to an integer, truncating decimal part
    let int_B = parseInt(b); // parseInt truncates for positive numbers, behaves differently for negative. Math.trunc() is safer but parseInt is common for basic truncation.

    // 3. Calculate sum of double_A and original double B
    let double_sum = double_A + b;

    // 4. Calculate sum of original integer A and int_B
    let int_sum = a + int_B;

    // Print results with specified formatting
    console.log(double_A.toFixed(2)); // toFixed(2) formats to two decimal places
    console.log(int_B);
    console.log(double_sum.toFixed(2));
    console.log(int_sum);
}

// Standard input/output for competitive programming environments in Node.js
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const parts = line.split(' ');
    const a = parseInt(parts[0]);  // Convert first part to integer
    const b = parseFloat(parts[1]); // Convert second part to float
    performTypeCasting(a, b);
    rl.close(); // Close the readline interface after processing one line
});

```