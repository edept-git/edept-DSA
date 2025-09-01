# Solutions for Mirror, Mirror on the Wall

### Approach
The most efficient way to check if a string is a palindrome is using the two-pointer technique. We initialize two pointers: one at the beginning of the string (let's call it `left_ptr`) and one at the end of the string (let's call it `right_ptr`). We then enter a loop that continues as long as `left_ptr` is less than `right_ptr`. Inside the loop, we compare the characters at `s[left_ptr]` and `s[right_ptr]`. If these characters are not equal, the string is not a palindrome, and we can immediately return `false` (or indicate "No"). If they are equal, we move `left_ptr` one step to the right and `right_ptr` one step to the left, effectively narrowing our comparison range. If the loop completes without finding any mismatches, it means all corresponding characters matched, and thus the string is a palindrome, so we return `true` (or indicate "Yes").

This algorithm uses no additional data structures beyond the input string itself.
*   **Time Complexity**: O(N), where N is the length of the string. In the worst case, we traverse roughly half the string (N/2 comparisons).
*   **Space Complexity**: O(1), as we only use a few constant-space variables (the pointers).

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

// Function to check if a string is a palindrome
bool isPalindrome(char* s) {
    int left = 0;
    int right = strlen(s) - 1;

    while (left < right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

int main() {
    char s[1001]; // Max length 1000 + null terminator
    scanf("%s", s);

    if (isPalindrome(s)) {
        printf("Yes\n");
    } else {
        printf("No\n");
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <algorithm> 

// Function to check if a string is a palindrome
bool isPalindrome(const std::string& s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

int main() {
    std::string s;
    std::cin >> s;

    if (isPalindrome(s)) {
        std::cout << "Yes" << std::endl;
    } else {
        std::cout << "No" << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to check if a string is a palindrome
    public static boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.next(); // Reads a single word

        if (isPalindrome(s)) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }

        scanner.close();
    }
}
```

## Python Solution
```python
def is_palindrome(s: str) -> bool:
    """
    Checks if a given string is a palindrome.
    """
    left = 0
    right = len(s) - 1

    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

if __name__ == "__main__":
    s = input()

    if is_palindrome(s):
        print("Yes")
    else:
        print("No")
```

## JavaScript Solution
```javascript
// Function to check if a string is a palindrome
function isPalindrome(s) {
    let left = 0;
    let right = s.length - 1;

    while (left < right) {
        if (s[left] !== s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}

// Read input from stdin
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    if (isPalindrome(line)) {
        console.log("Yes");
    } else {
        console.log("No");
    }
    rl.close(); // Close the interface after processing one line
});
```