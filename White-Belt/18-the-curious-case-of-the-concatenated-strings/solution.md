# Solutions for The Curious Case of the Concatenated Strings

### Approach
The solution involves using string variables to store the input strings.  String concatenation is achieved using the '+' operator (or equivalent in different languages). The time complexity is O(m+n), where m and n are the lengths of the input strings, as we iterate through each string once during the concatenation. Space complexity is O(m+n) as well, to store the concatenated string.

## C Solution
```c
#include <stdio.h>
#include <string.h>

void concatenateStrings(char str1[], char str2[]) {
    printf("%s%s", str1, str2);
}

int main() {
    char str1[101], str2[101];
    scanf("%s %s", str1, str2);
    concatenateStrings(str1, str2);
    printf("\n");
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

using namespace std;

void concatenateStrings(string str1, string str2) {
    cout << str1 + str2 << endl;
}

int main() {
    string str1, str2;
    cin >> str1 >> str2;
    concatenateStrings(str1, str2);
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class ConcatenateStrings {

    public static void concatenateStrings(String str1, String str2) {
        System.out.println(str1 + str2);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str1 = scanner.next();
        String str2 = scanner.next();
        concatenateStrings(str1, str2);
        scanner.close();
    }
}
```

## Python Solution
```python
def concatenate_strings(str1, str2):
    print(str1 + str2)

if __name__ == "__main__":
    str1, str2 = input().split()
    concatenate_strings(str1, str2)
```

## JavaScript Solution
```javascript
function concatenateStrings(str1, str2) {
  console.log(str1 + str2);
}

const input = process.argv.slice(2);
concatenateStrings(input[0], input[1]);
```