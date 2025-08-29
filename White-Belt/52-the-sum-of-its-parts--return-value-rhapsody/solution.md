# Solutions for The Sum of Its Parts:  Return Value Rhapsody

### Approach
The solution uses a simple function that takes two integer arguments and returns their sum using the '+' operator.  This approach has a time complexity of O(1) and a space complexity of O(1) because it performs a single arithmetic operation and uses a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int sum(int a, int b) {
  return a + b;
}

int main() {
  int a, b;
  scanf("%d %d", &a, &b);
  printf("%d\n", sum(a, b));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sum(int a, int b) {
  return a + b;
}

int main() {
  int a, b;
  std::cin >> a >> b;
  std::cout << sum(a, b) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Sum {

    public static int sum(int a, int b) {
        return a + b;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        System.out.println(sum(a, b));
        scanner.close();
    }
}
```

## Python Solution
```python
def sum(a, b):
    return a + b

a, b = map(int, input().split())
print(sum(a, b))
```

## JavaScript Solution
```javascript
function sum(a, b) {
  return a + b;
}

const input = require('readline-sync').prompt().split(' ').map(Number);
console.log(sum(input[0], input[1]));
```