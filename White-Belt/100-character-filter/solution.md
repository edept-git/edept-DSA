# Solutions for Character Filter

### Approach
The problem requires removing all occurrences of a specific character from an input string. A straightforward approach is to iterate through each character of the original string. For each character, we compare it with the character to be removed. If the character from the string is *not* the character to be removed, we append it to a new result string. After iterating through all characters of the original string, the new string will contain all characters except the specified one. This new string is then printed as the output.
This approach uses a single loop, making its time complexity O(N), where N is the length of the input string. The space complexity is also O(N) in the worst case (if no characters are removed or if we're building a new string explicitly), or O(1) if modifying in-place (not typical for string building in all languages or if immutable strings are used, but for new string construction, it's O(N)). Given the constraints (string length up to 100), this is highly efficient.

## C Solution
```c
#include <stdio.h>
#include <string.h>

// Function to remove all occurrences of a character from a string
void filterString(const char *original, char charToRemove, char *result) {
    int i = 0;
    int j = 0;
    while (original[i] != '\0') {
        if (original[i] != charToRemove) {
            result[j] = original[i];
            j++;
        }
        i++;
    }
    result[j] = '\0'; // Null-terminate the new string
}

int main() {
    char inputString[101]; // Max 100 chars + null terminator
    char charToRemove;
    char filteredString[101];

    // Read the input string
    scanf("%s", inputString);

    // Read the character to remove (note the space before %c to consume newline)
    scanf(" %c", &charToRemove);

    // Call the logic function
    filterString(inputString, charToRemove, filteredString);

    // Print the result
    printf("%s\n", filteredString);

    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Function to remove all occurrences of a character from a string
std::string filterString(const std::string& original, char charToRemove) {
    std::string result = ""; // Initialize an empty string
    for (char c : original) {
        if (c != charToRemove) {
            result += c; // Append character if it's not the one to remove
        }
    }
    return result;
}

int main() {
    std::string inputString;
    char charToRemove;

    // Read the input string
    std::cin >> inputString;

    // Read the character to remove
    std::cin >> charToRemove;

    // Call the logic function
    std::string filteredString = filterString(inputString, charToRemove);

    // Print the result
    std::cout << filteredString << std::endl;

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to remove all occurrences of a character from a string
    public static String filterString(String original, char charToRemove) {
        StringBuilder result = new StringBuilder();
        for (char c : original.toCharArray()) {
            if (c != charToRemove) {
                result.append(c);
            }
        }
        return result.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the input string
        String inputString = scanner.next();

        // Read the character to remove
        char charToRemove = scanner.next().charAt(0);

        // Call the logic function
        String filteredString = filterString(inputString, charToRemove);

        // Print the result
        System.out.println(filteredString);

        scanner.close();
    }
}

```

## Python Solution
```python
def filter_string(original_string, char_to_remove):
    """
    Removes all occurrences of a specific character from a string.
    """
    result = [] # Using a list of characters for efficient building, then join
    for char in original_string:
        if char != char_to_remove:
            result.append(char)
    return "".join(result)

def main():
    # Read the input string
    input_string = input()

    # Read the character to remove
    # input() reads a string, take the first character
    char_to_remove = input()[0]

    # Call the logic function
    filtered_string = filter_string(input_string, char_to_remove)

    # Print the result
    print(filtered_string)

if __name__ == "__main__":
    main()

```

## JavaScript Solution
```javascript
// For Node.js environment
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];

rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    main();
});

// Function to remove all occurrences of a character from a string
function filterString(original, charToRemove) {
    let result = '';
    for (let i = 0; i < original.length; i++) {
        if (original[i] !== charToRemove) {
            result += original[i];
        }
    }
    return result;
}

function main() {
    const inputString = inputLines[0];
    // charToRemove will be the first character of the second input line
    const charToRemove = inputLines[1][0]; 

    // Call the logic function
    const filteredString = filterString(inputString, charToRemove);

    // Print the result
    console.log(filteredString);
}

```