# Solutions for Double Trouble: The Return of the Duplicator

### Approach
The problem asks us to double an integer using a function. The approach is straightforward:
1.  Define a function (e.g., `doubleValue` or `duplicateNumber`) that accepts one integer parameter.
2.  Inside this function, multiply the input integer by 2.
3.  Return the calculated result from the function.
4.  In the `main` function (or equivalent entry point), read an integer from standard input.
5.  Call the `doubleValue` function, passing the read integer as an argument.
6.  Store the returned value in a variable.
7.  Print the stored result to standard output.

This approach uses constant extra space for variables (O(1)) and performs a single multiplication, making the time complexity O(1). No complex data structures are required.

## C Solution
```c
#include <stdio.h>

// Function to double an integer
int doubleValue(int n) {
    return n * 2;
}

int main() {
    int inputNum;
    // Read the integer from standard input
    scanf("%d", &inputNum);

    // Call the function and store the returned value
    int doubledNum = doubleValue(inputNum);

    // Print the doubled value
    printf("%d\n", doubledNum);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to double an integer
int doubleValue(int n) {
    return n * 2;
}

int main() {
    int inputNum;
    // Read the integer from standard input
    std::cin >> inputNum;

    // Call the function and store the returned value
    int doubledNum = doubleValue(inputNum);

    // Print the doubled value
    std::cout << doubledNum << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to double an integer
    public static int doubleValue(int n) {
        return n * 2;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the integer from standard input
        int inputNum = scanner.nextInt();

        // Call the function and store the returned value
        int doubledNum = doubleValue(inputNum);

        // Print the doubled value
        System.out.println(doubledNum);

        scanner.close();
    }
}
```

## Python Solution
```python
# Function to double an integer
def double_value(n):
    return n * 2

def main():
    # Read the integer from standard input
    input_num = int(input())

    # Call the function and store the returned value
    doubled_num = double_value(input_num)

    # Print the doubled value
    print(doubled_num)

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Function to double an integer
function doubleValue(n) {
    return n * 2;
}

// Main function to handle I/O and call logic
function main() {
    // Read the integer from standard input (Node.js style for competitive programming)
    // Assumes input is provided via stdin (file descriptor 0)
    // The trim() is important to remove any trailing newlines.
    const inputNum = parseInt(require('fs').readFileSync(0, 'utf8').trim(), 10);

    // Call the logic function
    const doubledNum = doubleValue(inputNum);

    // Print the result to standard output
    console.log(doubledNum);
}

// Execute the main function
main();
```