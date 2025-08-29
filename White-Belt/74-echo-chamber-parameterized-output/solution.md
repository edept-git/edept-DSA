# Solutions for Echo Chamber: Parameterized Output

### Approach
The program reads the string and integer from standard input. The core logic involves iterating from 0 to the specified integer (exclusive) and printing the string in each iteration. The time complexity is O(n), where n is the integer input. The space complexity is O(1) as it only stores the input string and integer.

## C Solution
```c
#include <stdio.h>
#include <string.h>

void echo_string(char str[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%s\n", str);
    }
}

int main() {
    char str[100];
    int n;

    scanf("%s %d", str, &n);

    echo_string(str, n);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

void echoString(std::string str, int n) {
    for (int i = 0; i < n; i++) {
        std::cout << str << std::endl;
    }
}

int main() {
    std::string str;
    int n;

    std::cin >> str >> n;

    echoString(str, n);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {
    public static void echoString(String str, int n) {
        for (int i = 0; i < n; i++) {
            System.out.println(str);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.next();
        int n = scanner.nextInt();

        echoString(str, n);

        scanner.close();
    }
}
```

## Python Solution
```python
def echo_string(string, n):
    for _ in range(n):
        print(string)

if __name__ == "__main__":
    string, n = input().split()
    n = int(n)
    echo_string(string, n)
```

## JavaScript Solution
```javascript
function echoString(str, n) {
    for (let i = 0; i < n; i++) {
        console.log(str);
    }
}

const input = require('fs').readFileSync('/dev/stdin', 'utf8');
const [str, n] = input.trim().split(' ');

echoString(str, parseInt(n));
```