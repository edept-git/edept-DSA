# Solutions for Casting Chronicles: Int to Float, Float to Int

### Approach
The approach to solving this problem is straightforward and focuses directly on demonstrating type casting. First, we will read the integer value and the floating-point value from the standard input. To convert the integer to a floating-point number, most languages will perform an implicit conversion if assigned to a floating-point variable, or an explicit cast can be used for clarity. The result will be the original integer value represented with a decimal component (e.g., `15` becomes `15.0`). Next, to convert the floating-point number to an integer, an explicit type cast is required in most languages. This conversion typically truncates the decimal part, effectively rounding down towards zero (e.g., `5.75` becomes `5`, and `-3.2` becomes `-3`). Finally, both converted values are printed to standard output on separate lines.

**Data Structures**: No complex data structures are required; we only use primitive integer and floating-point variables.

**Time Complexity**: O(1). The solution involves a fixed number of input operations, type conversions, and output operations, all of which take constant time regardless of the input values' magnitude.

**Space Complexity**: O(1). The solution uses a fixed amount of memory to store a few primitive variables, independent of the input values.

## C Solution
```c
#include <stdio.h>

// Function to perform type casting and print results
void performCasting(int intValue, double doubleValue) {
    // 1. Convert integer to double
    double intAsDouble = (double)intValue;
    printf("%.6lf\n", intAsDouble); // Print with 6 decimal places for clarity

    // 2. Convert double to integer
    int doubleAsInt = (int)doubleValue;
    printf("%d\n", doubleAsInt);
}

int main() {
    int intInput;
    double doubleInput;

    // Read integer input
    if (scanf("%d", &intInput) != 1) {
        return 1; // Error reading input
    }

    // Read double input
    if (scanf("%lf", &doubleInput) != 1) {
        return 1; // Error reading input
    }

    // Call the casting function
    performCasting(intInput, doubleInput);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <iomanip> // For std::fixed and std::setprecision

// Function to perform type casting and print results
void performCasting(int intValue, double doubleValue) {
    // 1. Convert integer to double
    double intAsDouble = static_cast<double>(intValue);
    std::cout << std::fixed << std::setprecision(6) << intAsDouble << std::endl;

    // 2. Convert double to integer
    int doubleAsInt = static_cast<int>(doubleValue);
    std::cout << doubleAsInt << std::endl;
}

int main() {
    int intInput;
    double doubleInput;

    // Read integer input
    std::cin >> intInput;

    // Read double input
    std::cin >> doubleInput;

    // Call the casting function
    performCasting(intInput, doubleInput);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to perform type casting and print results
    public static void performCasting(int intValue, double doubleValue) {
        // 1. Convert integer to double
        double intAsDouble = (double)intValue;
        System.out.printf("%.6f%n", intAsDouble);

        // 2. Convert double to integer
        int doubleAsInt = (int)doubleValue;
        System.out.println(doubleAsInt);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read integer input
        int intInput = scanner.nextInt();

        // Read double input
        double doubleInput = scanner.nextDouble();

        // Call the casting function
        performCasting(intInput, doubleInput);

        scanner.close();
    }
}
```

## Python Solution
```python
def perform_casting(int_value, double_value):
    # 1. Convert integer to float
    int_as_float = float(int_value)
    print(f"{int_as_float:.6f}") # Print with 6 decimal places

    # 2. Convert float to integer
    float_as_int = int(double_value)
    print(float_as_int)

if __name__ == '__main__':
    # Read integer input
    int_input = int(input())

    # Read float input
    double_input = float(input())

    # Call the casting function
    perform_casting(int_input, double_input)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let lines = [];
rl.on('line', (line) => {
    lines.push(line);
});

rl.on('close', () => {
    // Function to perform type casting and print results
    function performCasting(intValue, doubleValue) {
        // 1. Convert integer to float (JavaScript numbers are floats by default)
        // Explicit conversion can be seen as Number(intValue) for clarity.
        let intAsFloat = Number(intValue); 
        console.log(intAsFloat.toFixed(6)); // Format to 6 decimal places as a string

        // 2. Convert float to integer (truncates decimal part)
        let floatAsInt = Math.trunc(doubleValue); 
        console.log(floatAsInt);
    }

    // Read integer input
    let intInput = parseInt(lines[0], 10);

    // Read float input
    let doubleInput = parseFloat(lines[1]);

    // Call the casting function
    performCasting(intInput, doubleInput);
});
```