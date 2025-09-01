# Solutions for String Case Flipper

### Approach
To solve this problem, we will iterate through each character of the input string. For each character, we will apply conditional logic:
1.  If the character is an uppercase letter, we convert it to its lowercase equivalent.
2.  If the character is a lowercase letter, we convert it to its uppercase equivalent.
3.  If the character is neither an uppercase nor a lowercase letter (e.g., a number, symbol, or space), we leave it unchanged.
We will build a new string by appending these processed characters. Finally, we return this new string.

**Algorithm:**
1. Initialize an empty result string or character buffer.
2. Iterate through each character `c` in the input string.
3. For each `c`:
    a. Check if `c` is an uppercase letter. If true, convert `c` to lowercase and append to result.
    b. Else, check if `c` is a lowercase letter. If true, convert `c` to uppercase and append to result.
    c. Else (if `c` is not an alphabet), append `c` as is to result.
4. Return the result string.

**Data Structures:**
A string (or character array) for input and for building the output.

**Time Complexity:**
O(N), where N is the length of the input string. We visit each character exactly once.

**Space Complexity:**
O(N), where N is the length of the input string. This is because we create a new string to store the result.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h> // For islower, isupper, tolower, toupper
#include <stdlib.h> // For malloc, free

// Function to swap the case of characters in a string
char* swapCase(const char* s) {
    if (s == NULL) {
        return NULL;
    }

    size_t len = strlen(s);
    char* result = (char*)malloc(sizeof(char) * (len + 1)); // +1 for null terminator
    if (result == NULL) {
        return NULL; // Memory allocation failed
    }

    for (size_t i = 0; i < len; i++) {
        if (islower((unsigned char)s[i])) {
            result[i] = (char)toupper((unsigned char)s[i]);
        } else if (isupper((unsigned char)s[i])) {
            result[i] = (char)tolower((unsigned char)s[i]);
        } else {
            result[i] = s[i];
        }
    }
    result[len] = '\0'; // Null-terminate the result string
    return result;
}

int main() {
    char input[101]; // Max 100 chars + null terminator
    if (fgets(input, sizeof(input), stdin) == NULL) {
        return 1; // Error reading input
    }

    // Remove trailing newline character if present
    input[strcspn(input, "\n")] = 0;

    char* output = swapCase(input);
    if (output != NULL) {
        printf("%s\n", output);
        free(output); // Free allocated memory
    } else {
        // Handle error (e.g., malloc failed)
        return 1;
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <cctype> // For islower, isupper, tolower, toupper

// Function to swap the case of characters in a string
std::string swapCase(const std::string& s) {
    std::string result = "";
    for (char c : s) {
        if (std::islower(c)) {
            result += static_cast<char>(std::toupper(c));
        } else if (std::isupper(c)) {
            result += static_cast<char>(std::tolower(c));
        } else {
            result += c;
        }
    }
    return result;
}

int main() {
    std::string input;
    std::getline(std::cin, input);
    std::string output = swapCase(input);
    std::cout << output << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to swap the case of characters in a string
    public static String swapCase(String s) {
        if (s == null || s.isEmpty()) {
            return s;
        }

        StringBuilder result = new StringBuilder(s.length());
        for (char c : s.toCharArray()) {
            if (Character.isLowerCase(c)) {
                result.append(Character.toUpperCase(c));
            } else if (Character.isUpperCase(c)) {
                result.append(Character.toLowerCase(c));
            } else {
                result.append(c);
            }
        }
        return result.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();
        String output = swapCase(input);
        System.out.println(output);
        scanner.close();
    }
}
```

## Python Solution
```python
def swapCase(s: str) -> str:
    """
    Swaps the case of each alphabetic character in a string.
    Lowercase letters become uppercase, and uppercase letters become lowercase.
    Non-alphabetic characters remain unchanged.
    """
    result_chars = []
    for char in s:
        if char.islower():
            result_chars.append(char.upper())
        elif char.isupper():
            result_chars.append(char.lower())
        else:
            result_chars.append(char)
    return "".join(result_chars)

if __name__ == "__main__":
    input_string = input()
    output_string = swapCase(input_string)
    print(output_string)
```

## JavaScript Solution
```javascript
function swapCase(s) {
    if (!s) {
        return s;
    }

    let result = '';
    for (let i = 0; i < s.length; i++) {
        const char = s[i];
        // Check if the character is an alphabetic character
        if (char >= 'a' && char <= 'z') {
            result += char.toUpperCase();
        } else if (char >= 'A' && char <= 'Z') {
            result += char.toLowerCase();
        } else {
            result += char;
        }
    }
    return result;
}

// Read input from stdin
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const output = swapCase(line);
    console.log(output);
    rl.close();
});
```