# Solutions for Reverse That String!

### Approach
The most straightforward approach is to iterate through the input string from the last character to the first, appending each character to a new string. This approach uses a single string as a data structure and has a time complexity of O(n) where n is the length of the string, due to the single pass through the string. The space complexity is also O(n) because we create a new string of the same length as the input.

## C Solution
```c
#include <stdio.h>
#include <string.h>

char* reverseString(char* str) {
    int len = strlen(str);
    char* reversed = (char*)malloc((len + 1) * sizeof(char));
    for (int i = 0; i < len; i++) {
        reversed[i] = str[len - 1 - i];
    }
    reversed[len] = '\0';
    return reversed;
}

int main() {
    char str[1001];
    scanf("%s", str);
    char* reversedStr = reverseString(str);
    printf("%s\n", reversedStr);
    free(reversedStr);
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
    std::string str;
    std::cin >> str;
    std::cout << reverseString(str) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.*;

public class ReverseString {
    public static String reverseString(String str) {
        return new StringBuilder(str).reverse().toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        System.out.println(reverseString(str));
        scanner.close();
    }
}
```

## Python Solution
```python
def reverse_string(s):
    return s[::-1]

if __name__ == "__main__":
    s = input()
    print(reverse_string(s))
```

## JavaScript Solution
```javascript
function reverseString(str) {
  return str.split('').reverse().join('');
}

const str = process.argv[2];
console.log(reverseString(str));
```