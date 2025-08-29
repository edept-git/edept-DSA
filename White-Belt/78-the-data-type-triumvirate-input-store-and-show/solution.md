# Solutions for The Data Type Triumvirate: Input, Store, and Show!

### Approach
This problem is designed to introduce fundamental programming concepts: variables, data types, and basic I/O. The approach is straightforward. First, declare three variables: one for an integer (e.g., `int`), one for a floating-point number (e.g., `float` or `double`), and one for a string (e.g., `char[]` or `std::string`). The `main` function is responsible for reading these three values from standard input. After reading, these values are passed to a separate utility function, which encapsulates the core logic. This function then prints the initial message, followed by each stored value labeled with its type, and finally, prints the original integer value incremented by one. This separation of concerns (I/O in `main`, processing/printing in a dedicated function) is a good practice. The time complexity for this solution is O(1) because it involves a fixed number of operations (input, assignments, a single arithmetic operation, and output) regardless of the specific input values. The space complexity is also O(1) as it uses a constant amount of memory for a few variables to store the inputs.

## C Solution
```c
#include <stdio.h>
#include <string.h>

// Core logic function to process and print the data
void processAndPrint(int integer_val, double float_val, char *string_val) {
    printf("You entered:\n");
    printf("Integer: %d\n", integer_val);
    printf("Float: %.2lf\n", float_val); // Print with 2 decimal places
    printf("String: %s\n", string_val);
    printf("Next Integer: %d\n", integer_val + 1);
}

int main() {
    int num;
    double dec;
    char word[11]; // Max 10 chars + null terminator

    // Read input
    scanf("%d", &num);
    scanf("%lf", &dec);
    scanf("%s", word);

    // Call the core logic function
    processAndPrint(num, dec, word);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <iomanip> // For std::fixed and std::setprecision

// Core logic function to process and print the data
void processAndPrint(int integer_val, double float_val, std::string string_val) {
    std::cout << "You entered:" << std::endl;
    std::cout << "Integer: " << integer_val << std::endl;
    std::cout << "Float: " << std::fixed << std::setprecision(2) << float_val << std::endl;
    std::cout << "String: " << string_val << std::endl;
    std::cout << "Next Integer: " << integer_val + 1 << std::endl;
}

int main() {
    int num;
    double dec;
    std::string word;

    // Read input
    std::cin >> num;
    std::cin >> dec;
    std::cin >> word;

    // Call the core logic function
    processAndPrint(num, dec, word);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Core logic function to process and print the data
    public static void processAndPrint(int integer_val, double float_val, String string_val) {
        System.out.println("You entered:");
        System.out.println("Integer: " + integer_val);
        System.out.printf("Float: %.2f%n", float_val); // Print with 2 decimal places
        System.out.println("String: " + string_val);
        System.out.println("Next Integer: " + (integer_val + 1));
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read input
        int num = scanner.nextInt();
        double dec = scanner.nextDouble();
        String word = scanner.next();

        // Call the core logic function
        processAndPrint(num, dec, word);

        scanner.close();
    }
}
```

## Python Solution
```python
def process_and_print(integer_val, float_val, string_val):
    # Core logic function to process and print the data
    print("You entered:")
    print(f"Integer: {integer_val}")
    print(f"Float: {float_val:.2f}") # Print with 2 decimal places
    print(f"String: {string_val}")
    print(f"Next Integer: {integer_val + 1}")

if __name__ == '__main__':
    # Read input
    num = int(input())
    dec = float(input())
    word = input()

    # Call the core logic function
    process_and_print(num, dec, word)
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
    // Read input
    let num = parseInt(lines[0]);
    let dec = parseFloat(lines[1]);
    let word = lines[2];

    // Call the core logic function
    processAndPrint(num, dec, word);
});

// Core logic function to process and print the data
function processAndPrint(integer_val, float_val, string_val) {
    console.log("You entered:");
    console.log(`Integer: ${integer_val}`);
    console.log(`Float: ${float_val.toFixed(2)}`); // Print with 2 decimal places
    console.log(`String: ${string_val}`);
    console.log(`Next Integer: ${integer_val + 1}`);
}
```