# Solutions for Mirror Mirror on the String!

### Approach
The approach uses two pointers, one at the beginning and one at the end of the string.  It iterates inwards, comparing characters after converting them to lowercase and checking if they are alphanumeric. If a mismatch is found or the pointers cross, the function returns `false`; otherwise, it returns `true` after the pointers have processed the entire string.  The time complexity is O(n), where n is the length of the string, and the space complexity is O(1).

## C Solution
```c
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdbool.h>

bollean isPalindrome(char *str) {
    int left = 0;
    int right = strlen(str) - 1;

    while (left < right) {
        while (left < right && !isalnum(str[left])) left++;
        while (left < right && !isalnum(str[right])) right--;
        if (tolower(str[left]) != tolower(str[right])) return false;
        left++;
        right--;
    }
    return true;
}

int main() {
    char str[1001];
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; 
    if (isPalindrome(str)) {
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

using namespace std;

boolean isPalindrome(string s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        while (left < right && !isalnum(s[left])) left++;
        while (left < right && !isalnum(s[right])) right--;
        if (tolower(s[left]) != tolower(s[right])) return false;
        left++;
        right--;
    }
    return true;
}

int main() {
    string s;
    getline(cin, s);
    if (isPalindrome(s)) {
        cout << "true" << endl;
    } else {
        cout << "false" << endl;
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
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) return false;
            left++;
            right--;
        }
        return true;
    }
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        Solution sol = new Solution();
        System.out.println(sol.isPalindrome(s));
        sc.close();
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
function isPalindrome(str) {
  str = str.toLowerCase().replace(/[^a-z0-9]/g, '');
  return str === str.split('').reverse().join('');
}

let str = require('readline-sync').question();
console.log(isPalindrome(str));
```