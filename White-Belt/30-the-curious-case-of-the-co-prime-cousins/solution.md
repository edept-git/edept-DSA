# Solutions for The Curious Case of the Co-prime Cousins

### Approach
The problem can be solved by finding the GCD of the two input numbers.  We can use the Euclidean algorithm for efficient GCD calculation. If the GCD is 1, the numbers are co-prime; otherwise, they are not. The Euclidean algorithm has a time complexity of O(log(min(a, b))). The space complexity is O(1) as we only use a few variables.

## C Solution
```c
#include <stdio.h>

int gcd(int a, int b) {
  if (b == 0) {
    return a;
  }
  return gcd(b, a % b);
}

int main() {
  int a, b;
  scanf("%d %d", &a, &b);
  if (gcd(a, b) == 1) {
    printf("Yes");
  } else {
    printf("No");
  }
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int gcd(int a, int b) {
  if (b == 0) {
    return a;
  }
  return gcd(b, a % b);
}

int main() {
  int a, b;
  std::cin >> a >> b;
  if (gcd(a, b) == 1) {
    std::cout << "Yes";
  } else {
    std::cout << "No";
  }
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class CoPrime {

    public static int gcd(int a, int b) {
        if (b == 0) {
            return a;
        }
        return gcd(b, a % b);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        if (gcd(a, b) == 1) {
            System.out.println("Yes");
        } else {
            System.out.println("No");
        }
        scanner.close();
    }
}
```

## Python Solution
```python
import math

def gcd(a, b):
  if b == 0:
    return a
  return gcd(b, a % b)

a, b = map(int, input().split())
if gcd(a, b) == 1:
  print("Yes")
else:
  print("No")
```

## JavaScript Solution
```javascript
function gcd(a, b) {
  if (b === 0) {
    return a;
  }
  return gcd(b, a % b);
}

const input = require('readline-sync').question().split(' ');
const a = parseInt(input[0]);
const b = parseInt(input[1]);
if (gcd(a, b) === 1) {
  console.log('Yes');
} else {
  console.log('No');
}
```