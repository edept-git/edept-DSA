# Solutions for Remainder Riddle

### Approach
The solution uses the modulo operator (%) to find the remainder when `a` is divided by `b`.  The modulo operator returns the remainder of the division. This approach has a time complexity of O(1) and a space complexity of O(1) because it involves a single arithmetic operation.

## C Solution
```c
#include <stdio.h>

int findRemainder(int a, int b) {
  return a % b;
}

int main() {
  int a, b;
  scanf("%d %d", &a, &b);
  printf("%d\n", findRemainder(a, b));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int findRemainder(int a, int b) {
  return a % b;
}

int main() {
  int a, b;
  std::cin >> a >> b;
  std::cout << findRemainder(a, b) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Remainder {
    public static int findRemainder(int a, int b) {
        return a % b;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        System.out.println(findRemainder(a, b));
        scanner.close();
    }
}
```

## Python Solution
```python
def find_remainder(a, b):
  return a % b

a, b = map(int, input().split())
print(find_remainder(a, b))
```

## JavaScript Solution
```javascript
function findRemainder(a, b) {
  return a % b;
}

const input = require('readline-sync').question().split(' ').map(Number);
const a = input[0];
const b = input[1];
console.log(findRemainder(a,b));
```