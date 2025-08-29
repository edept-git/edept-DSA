# Solutions for Echo Chamber

### Approach
The solution uses standard input/output functions to read a line of text from the standard input (stdin) and print it to the standard output (stdout).  No complex data structures or algorithms are needed. The time complexity is O(n), where n is the length of the input string, due to the single iteration through the input line. The space complexity is O(n) to store the input string.

## C Solution
```c
#include <stdio.h>
#include <string.h>

void echo(char *input) {
    printf("%s\n", input);
}

int main() {
    char input[1001];
    fgets(input, sizeof(input), stdin);
    input[strcspn(input, "\n")] = 0; //remove trailing newline
    echo(input);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

void echo(std::string input) {
    std::cout << input << std::endl;
}

int main() {
    std::string input;
    std::getline(std::cin, input);
    echo(input);
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Echo {
    public static void echo(String input) {
        System.out.println(input);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String input = scanner.nextLine();
        echo(input);
        scanner.close();
    }
}
```

## Python Solution
```python
def echo(input_string):
    print(input_string)

if __name__ == "__main__":
    input_string = input()
    echo(input_string)
```

## JavaScript Solution
```javascript
function echo(input) {
  console.log(input);
}

const input = require('readline-sync').prompt().trim();
echo(input);
```