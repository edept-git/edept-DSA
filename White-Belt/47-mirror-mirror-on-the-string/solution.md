# Solutions for Mirror, Mirror on the String

### Approach
The solution uses a two-pointer approach.  We first preprocess the string to remove non-alphanumeric characters and convert it to lowercase. Two pointers, one at the beginning and one at the end of the string, are then used to compare characters. If the characters at both pointers are equal, the pointers are moved towards the center; otherwise, the string is not a palindrome. The time complexity is O(n), where n is the length of the string, and the space complexity is O(1) if we modify the input string in place, or O(n) if we create a copy.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int isPalindrome(char *s) {
    int l = 0, r = strlen(s) - 1;
    while (l < r) {
        while (l < r && !isalnum(s[l])) l++;
        while (l < r && !isalnum(s[r])) r--;
        if (tolower(s[l]) != tolower(s[r])) return 0;
        l++;
        r--;
    }
    return 1;
}

int main() {
    char s[1001];
    scanf("%[^
]s", s);
    if (isPalindrome(s)) {
        printf("true\n");
    } else {
        printf("false\n");
    }
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>

bool isPalindrome(std::string s) {
    int l = 0, r = s.length() - 1;
    while (l < r) {
        while (l < r && !isalnum(s[l])) l++;
        while (l < r && !isalnum(s[r])) r--;
        if (tolower(s[l]) != tolower(s[r])) return false;
        l++;
        r--;
    }
    return true;
}

int main() {
    std::string s;
    std::getline(std::cin, s);
    if (isPalindrome(s)) {
        std::cout << "true" << std::endl;
    } else {
        std::cout << "false" << std::endl;
    }
    return 0;
}
```

## Java Solution
```java
import java.util.*;
import java.lang.*;

class Solution {
    public boolean isPalindrome(String s) {
        int l = 0, r = s.length() - 1;
        while (l < r) {
            while (l < r && !Character.isLetterOrDigit(s.charAt(l))) l++;
            while (l < r && !Character.isLetterOrDigit(s.charAt(r))) r--;
            if (Character.toLowerCase(s.charAt(l)) != Character.toLowerCase(s.charAt(r))) return false;
            l++;
            r--;
        }
        return true;
    }
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.nextLine();
        Solution sol = new Solution();
        System.out.println(sol.isPalindrome(s));
        scanner.close();
    }
}
```

## Python Solution
```python
import re

def isPalindrome(s):
    new_string = re.sub(r'[^a-zA-Z0-9]', '', s).lower()
    return new_string == new_string[::-1]

s = input()
print(isPalindrome(s))
```

## JavaScript Solution
```javascript
function isPalindrome(s) {
  s = s.toLowerCase().replace(/[^a-z0-9]/g, '');
  return s === s.split('').reverse().join('');
}

const readline = require('readline').createInterface({
    input: process.stdin,
    output: process.stdout,
});

readline.question('', (s) => {
  console.log(isPalindrome(s));
  readline.close();
});
```