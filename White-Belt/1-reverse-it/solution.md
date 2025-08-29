# Solutions for Reverse It!

### Approach
The most straightforward approach is to iterate through the input string from the last character to the first and append each character to a new string. This creates a reversed copy of the original string.  This approach has a time complexity of O(n) and a space complexity of O(n), where n is the length of the input string.

## C Solution
```c
#include <stdio.h>
#include <string.h>

char* reverseString(char* str) {
    int len = strlen(str);
    char* reversed = (char*)malloc(sizeof(char) * (len + 1));
    for (int i = 0; i < len; i++) {
        reversed[i] = str[len - 1 - i];
    }
    reversed[len] = '\0';
    return reversed;
}

int main() {
    char input[1001];
    scanf("%s", input);
    char* reversed = reverseString(input);
    printf("%s\n", reversed);
    free(reversed);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <algorithm>

std::string reverseString(std::string str) {
    std::reverse(str.begin(), str.end());
    return str;
}

int main() {
    std::string input;
    std::cin >> input;
    std::cout << reverseString(input) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class ReverseString {
    public static String reverseString(String str) {
        return new StringBuilder(str).reverse().toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();
        System.out.println(reverseString(input));
        scanner.close();
    }
}
```

## Python Solution
```python
def reverse_string(s):
    return s[::-1]

if __name__ == "__main__":
    input_str = input()
    reversed_str = reverse_string(input_str)
    print(reversed_str)
```

## JavaScript Solution
```javascript
function reverseString(str) {
  return str.split("").reverse().join("");
}

const input = require('readline-sync').prompt().trim();
console.log(reverseString(input));
```