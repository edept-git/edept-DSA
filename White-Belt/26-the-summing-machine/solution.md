# Solutions for The Summing Machine

### Approach
The solution uses a simple function that takes two integers as input and returns their sum.  No complex data structures are needed. The time complexity is O(1) and the space complexity is O(1) because the operation is performed directly without using any auxiliary data structures that grow with the input size.

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

public class SummingMachine {

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

const [a, b] = require('readline-sync').question("").split(' ').map(Number);
console.log(sum(a, b));
```