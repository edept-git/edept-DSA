# Solutions for Find the Greatest Common Divisor (GCD)

### Approach
The solution uses the Euclidean algorithm to find the GCD. The Euclidean algorithm is an efficient method for computing the greatest common divisor (GCD) of two integers. It's based on the principle that the GCD of two numbers does not change if the smaller number is subtracted from the larger number. This process is repeated until one of the numbers becomes zero. The other number is then the GCD.  The iterative approach is used for simplicity and readability, offering a time complexity of O(log(min(a, b))) and a space complexity of O(1).

## C Solution
```c
#include <stdio.h>

int gcd(int a, int b) {
    while (b) {
        a %= b;
        int temp = a;
        a = b;
        b = temp;
    }
    return a;
}

int main() {
    int a, b;
    scanf("%d %d", &a, &b);
    printf("%d\n", gcd(a, b));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int gcd(int a, int b) {
    while (b) {
        a %= b;
        int temp = a;
        a = b;
        b = temp;
    }
    return a;
}

int main() {
    int a, b;
    std::cin >> a >> b;
    std::cout << gcd(a, b) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class GCD {
    public static int gcd(int a, int b) {
        while (b != 0) {
            int temp = a % b;
            a = b;
            b = temp;
        }
        return a;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        System.out.println(gcd(a, b));
        scanner.close();
    }
}
```

## Python Solution
```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a

a, b = map(int, input().split())
print(gcd(a, b))
```

## JavaScript Solution
```javascript
function gcd(a, b) {
  while (b) {
    let temp = a % b;
    a = b;
    b = temp;
  }
  return a;
}

const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim().split(' ');
const a = parseInt(input[0]);
const b = parseInt(input[1]);
console.log(gcd(a,b));
```