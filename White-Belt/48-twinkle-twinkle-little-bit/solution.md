# Solutions for Twinkle Twinkle Little Bit

### Approach
Powers of 2 have only one bit set to 1 in their binary representation (e.g., 1, 2, 4, 8, 16 are 0001, 0010, 0100, 1000, 10000 in binary).  We can leverage this property using the bitwise AND operator. A number that is a power of 2, when ANDed with (n - 1), will result in 0.  This is because (n - 1) will have all bits to the right of the single set bit in n set to 1. The time complexity is O(1) and the space complexity is O(1).

## C Solution
```c
#include <stdio.h>

int isPowerOfTwo(int n) {
  return (n > 0) && ((n & (n - 1)) == 0);
}

int main() {
  int n;
  scanf("%d", &n);
  if (isPowerOfTwo(n)) {
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

bool isPowerOfTwo(int n) {
  return (n > 0) && ((n & (n - 1)) == 0);
}

int main() {
  int n;
  std::cin >> n;
  if (isPowerOfTwo(n)) {
    std::cout << "true" << std::endl;
  } else {
    std::cout << "false" << std::endl;
  }
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class PowerOfTwo {

    public static boolean isPowerOfTwo(int n) {
        return (n > 0) && ((n & (n - 1)) == 0);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        if (isPowerOfTwo(n)) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
        scanner.close();
    }
}
```

## Python Solution
```python
def isPowerOfTwo(n):
  return (n > 0) and ((n & (n - 1)) == 0)

n = int(input())
if isPowerOfTwo(n):
  print("true")
else:
  print("false")
```

## JavaScript Solution
```javascript
function isPowerOfTwo(n) {
  return (n > 0) && ((n & (n - 1)) === 0);
}

const n = parseInt(process.argv[2]);
if (isPowerOfTwo(n)) {
  console.log("true");
} else {
  console.log("false");
}
```