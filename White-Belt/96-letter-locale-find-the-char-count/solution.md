# Solutions for Letter Locale: Find the Char Count

### Approach
The most straightforward approach to solve this problem is to iterate through each character of the input string from beginning to end. For each character encountered during this iteration, we compare it with the given target character `c`. If the current character from the string matches `c`, we increment a dedicated counter variable. After the loop has processed every character in the string, the final value of the counter will represent the total number of occurrences of `c` in `s`.

**Algorithm:**
1. Initialize an integer variable, `count`, to 0.
2. Start a loop that iterates from the first character to the last character of the input string `s`.
3. In each iteration of the loop, retrieve the current character from `s`.
4. Compare this current character with the target character `c`.
5. If the two characters are identical (remembering that the comparison is case-sensitive), increment the `count` variable.
6. After the loop completes, return the final value of `count`.

**Data Structures:**
No complex data structures are required. We only use the input string itself and a simple integer variable to store the count.

**Time Complexity:**
O(N), where N is the length of the input string `s`. This is because the algorithm must examine each character of the string at least once to determine if it matches the target character.

**Space Complexity:**
O(1), as the amount of extra memory used (for variables like the counter and loop index) does not grow with the size of the input string. It remains constant regardless of N.

## C Solution
```c
#include <stdio.h>
#include <string.h>

// Function to count occurrences of a character in a string
int countChar(const char* s, char c) {
    int count = 0;
    int len = strlen(s);
    for (int i = 0; i < len; i++) {
        if (s[i] == c) {
            count++;
        }
    }
    return count;
}

int main() {
    char s[1001]; // Max length 1000 + null terminator
    char c;

    // Read the string (assumes no spaces based on constraints)
    scanf("%s", s);

    // Read the character, with a space before %c to consume any leftover whitespace (like newline)
    scanf(" %c", &c);

    int result = countChar(s, c);

    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <vector>

// Function to count occurrences of a character in a string
int countChar(const std::string& s, char c) {
    int count = 0;
    for (char current_char : s) { // Use a range-based for loop for elegant iteration
        if (current_char == c) {
            count++;
        }
    }
    return count;
}

int main() {
    std::string s;
    char c;

    // Read the string (assumes no spaces based on constraints)
    std::cin >> s;

    // Read the character
    std::cin >> c;

    int result = countChar(s, c);

    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to count occurrences of a character in a string
    public int countChar(String s, char c) {
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == c) {
                count++;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the string (assumes no spaces based on constraints)
        String s = scanner.next();

        // Read the character
        // scanner.next() reads the next token as a string, .charAt(0) takes its first character
        char c = scanner.next().charAt(0);

        Solution sol = new Solution();
        int result = sol.countChar(s, c);

        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def count_char(s: str, c: str) -> int:
    """
    Counts the occurrences of a character in a string.
    """
    count = 0
    for char in s:
        if char == c:
            count += 1
    return count

if __name__ == "__main__":
    # Read the string (assumes no spaces based on constraints)
    s = input()

    # Read the character (input() reads a line, so c will be a string of length 1)
    c = input()

    result = count_char(s, c)

    print(result)
```

## JavaScript Solution
```javascript
function countChar(s, c) {
    let count = 0;
    for (let i = 0; i < s.length; i++) {
        if (s[i] === c) {
            count++;
        }
    }
    return count;
}

// --- Standard competitive programming structure for JS on Node.js --- 
// Read all input lines
const inputLines = [];
require('readline').createInterface({
    input: process.stdin,
    output: process.stdout
}).on('line', line => {
    inputLines.push(line);
}).on('close', () => {
    // Once all input is read, call main logic
    main(inputLines);
});

function main(inputLines) {
    const s = inputLines[0]; // First line is the string
    const c = inputLines[1]; // Second line is the character (as a string of length 1)
    
    const result = countChar(s, c);
    console.log(result);
}
```