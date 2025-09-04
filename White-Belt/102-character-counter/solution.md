# Solutions for Character Counter

### Approach
The problem can be solved by iterating through each character of the input string. A counter variable, initialized to zero, will keep track of the occurrences. For each character in the string, it is compared with the target character. If they match (case-sensitive), the counter is incremented. After checking all characters in the string, the final value of the counter is printed as the result. This approach involves a single pass through the string, making its time complexity O(N), where N is the length of the string. The space complexity is O(1) as only a few variables are used, independent of the string's length.

## C Solution
```c
#include <stdio.h>
#include <string.h>

// Function to count occurrences of a character in a string
int countChar(const char* str, char target) {
    int count = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        if (str[i] == target) {
            count++;
        }
    }
    return count;
}

int main() {
    char inputString[1001]; // Max length 1000 + null terminator
    char targetChar;

    // Read the string
    // Using fgets to read the whole line including spaces
    if (fgets(inputString, sizeof(inputString), stdin) == NULL) {
        return 1; // Error reading input
    }

    // Remove the trailing newline character if present
    inputString[strcspn(inputString, "\n")] = 0;

    // Read the target character
    if (scanf(" %c", &targetChar) != 1) { // Space before %c to consume any leftover newline
        return 1; // Error reading input
    }

    // Call the core logic function
    int occurrences = countChar(inputString, targetChar);

    // Print the result
    printf("%d\n", occurrences);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Function to count occurrences of a character in a string
int countChar(const std::string& str, char target) {
    int count = 0;
    for (char c : str) {
        if (c == target) {
            count++;
        }
    }
    return count;
}

int main() {
    std::string inputString;
    char targetChar;

    // Read the string (can contain spaces)
    std::getline(std::cin, inputString);

    // Read the target character
    std::cin >> targetChar;

    // Call the core logic function
    int occurrences = countChar(inputString, targetChar);

    // Print the result
    std::cout << occurrences << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to count occurrences of a character in a string
    public static int countChar(String str, char target) {
        int count = 0;
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) == target) {
                count++;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the string
        String inputString = scanner.nextLine();

        // Read the target character
        // Read next token and get its first character
        char targetChar = scanner.next().charAt(0);

        // Call the core logic function
        int occurrences = countChar(inputString, targetChar);

        // Print the result
        System.out.println(occurrences);

        scanner.close();
    }
}
```

## Python Solution
```python
def count_char(s: str, target: str) -> int:
    """
    Counts the occurrences of a target character in a string.
    """
    count = 0
    for char in s:
        if char == target:
            count += 1
    return count

if __name__ == "__main__":
    # Read the string
    input_string = input()

    # Read the target character
    target_char = input()

    # Call the core logic function
    occurrences = count_char(input_string, target_char)

    # Print the result
    print(occurrences)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];

// Function to count occurrences of a character in a string
function countChar(str, target) {
    let count = 0;
    for (let i = 0; i < str.length; i++) {
        if (str[i] === target) {
            count++;
        }
    }
    return count;
}

rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    const inputString = inputLines[0];
    const targetChar = inputLines[1];

    // Call the core logic function
    const occurrences = countChar(inputString, targetChar);

    // Print the result
    console.log(occurrences);
});
```