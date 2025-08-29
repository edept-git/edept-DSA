# Solutions for Flipping the Least Significant Bit

### Approach
The most efficient way to flip the least significant bit of an integer is to use the XOR bitwise operator.  XORing a number with 1 will flip the LSB.  If the LSB is 0, it becomes 1; if it's 1, it becomes 0. This operation has a time complexity of O(1) and a space complexity of O(1) because it operates directly on the bits of the integer without needing additional data structures.

## C Solution
```c
#include <stdio.h>

int flipLSB(int n) {
  return n ^ 1;
}

int main() {
  int num;
  scanf("%d", &num);
  printf("%d\n", flipLSB(num));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int flipLSB(int n) {
  return n ^ 1;
}

int main() {
  int num;
  std::cin >> num;
  std::cout << flipLSB(num) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class FlipLSB {

    public static int flipLSB(int n) {
        return n ^ 1;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int num = scanner.nextInt();
        System.out.println(flipLSB(num));
        scanner.close();
    }
}
```

## Python Solution
```python
def flipLSB(n):
  return n ^ 1

num = int(input())
print(flipLSB(num))
```

## JavaScript Solution
```javascript
function flipLSB(n) {
  return n ^ 1;
}

const num = parseInt(readline());
console.log(flipLSB(num));
```