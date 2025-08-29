# Solutions for Scrub the String

### Approach
The most straightforward approach is to iterate through the input string character by character. We will maintain a new, empty string (or a similar data structure like a `StringBuilder` in Java, or an array of characters in Python/JavaScript that can be joined later). For each character in the original string, we check if it is *not* equal to the `charToRemove`. If it's not the character we want to remove, we append it to our new string. After processing all characters in the input string, the new string will contain all characters from the original string except for the specified character to be removed. Finally, this new string is returned. The time complexity for this approach is O(N), where N is the length of the input string, because we iterate through the string once. The space complexity is O(N) in the worst case (e.g., if no characters are removed, or if all characters are different from `charToRemove`), as we are building a new string that could be up to the same length as the original.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* removeChar(const char* s, char charToRemove) {
    if (s == NULL) {
        return NULL;
    }

    int len = strlen(s);
    char* result = (char*)malloc(len + 1); // Max possible length + null terminator
    if (result == NULL) {
        return NULL; // Memory allocation failed
    }

    int k = 0; // Index for the result string
    for (int i = 0; i < len; i++) {
        if (s[i] != charToRemove) {
            result[k++] = s[i];
        }
    }
    result[k] = '\0'; // Null-terminate the new string
    
    // Reallocate to save memory if needed, though not strictly required for correctness
    // char* final_result = (char*)realloc(result, k + 1);
    // if (final_result != NULL) {
    //     return final_result;
    // } else {
    //     return result; // realloc failed, return original result
    // }
    return result;
}

int main() {
    char inputString[1001];
    char charToRemoveStr[2]; // To read a single character as a string
    char charToRemove;

    // Read the input string
    if (fgets(inputString, sizeof(inputString), stdin) == NULL) {
        return 1;
    }
    // Remove trailing newline character if present
    inputString[strcspn(inputString, "\n")] = '\0';

    // Read the character to remove
    if (fgets(charToRemoveStr, sizeof(charToRemoveStr), stdin) == NULL) {
        return 1;
    }
    charToRemove = charToRemoveStr[0];

    char* result = removeChar(inputString, charToRemove);
    if (result != NULL) {
        printf("%s\n", result);
        free(result); // Free the dynamically allocated memory
    } else {
        printf("Error or NULL input.\n");
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <algorithm>

std::string removeChar(const std::string& s, char charToRemove) {
    std::string result = "";
    for (char c : s) {
        if (c != charToRemove) {
            result += c;
        }
    }
    return result;
}

int main() {
    std::string s;
    char charToRemove;

    // Read the input string
    std::getline(std::cin, s);

    // Read the character to remove
    // std::cin will read the char and leave the newline in the buffer.
    // We need to consume the newline character if there are further std::getline calls.
    // For this problem, we only have one string and one char input, so it's less critical.
    std::cin >> charToRemove;

    std::string result = removeChar(s, charToRemove);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    public String removeChar(String s, char charToRemove) {
        if (s == null || s.isEmpty()) {
            return s;
        }

        StringBuilder resultBuilder = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (c != charToRemove) {
                resultBuilder.append(c);
            }
        }
        return resultBuilder.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the input string
        String s = scanner.nextLine();

        // Read the character to remove
        // scanner.next() reads the next token, scanner.next().charAt(0) gets the first char
        char charToRemove = scanner.next().charAt(0);

        Solution sol = new Solution();
        String result = sol.removeChar(s, charToRemove);
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def remove_char(s: str, char_to_remove: str) -> str:
    if not s:
        return ""
    
    # Ensure char_to_remove is a single character string
    if len(char_to_remove) != 1:
        # This case is technically handled by constraints but good practice
        raise ValueError("char_to_remove must be a single character string")

    result_chars = []
    for char_s in s:
        if char_s != char_to_remove:
            result_chars.append(char_s)
    return "".join(result_chars)

if __name__ == "__main__":
    # Read the input string
    s = input()

    # Read the character to remove (input() reads a line, we take the first char)
    char_to_remove_input = input()
    char_to_remove = char_to_remove_input[0] if char_to_remove_input else ''

    result = remove_char(s, char_to_remove)
    print(result)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

function removeChar(s, charToRemove) {
    if (!s) {
        return "";
    }

    let result = '';
    for (let i = 0; i < s.length; i++) {
        if (s[i] !== charToRemove) {
            result += s[i];
        }
    }
    return result;
}

let lines = [];
rl.on('line', (line) => {
    lines.push(line);
}).on('close', () => {
    const s = lines[0];
    const charToRemove = lines[1][0]; // Take the first character of the second line

    const result = removeChar(s, charToRemove);
    console.log(result);
});
```