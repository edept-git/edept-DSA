# Solutions for Prime Time Detective

### Approach
The solution uses a simple iterative approach to check for primality.  We iterate from 2 up to the square root of the input number. If any number in this range divides the input number evenly, it's not prime.  The time complexity is O(√n), and the space complexity is O(1).

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>
#include <math.h>

boolean isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int n;
    scanf("%d", &n);
    printf("%s\n", isPrime(n) ? "true" : "false");
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <cmath>

bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int n;
    std::cin >> n;
    std::cout << (isPrime(n) ? "true" : "false") << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.lang.Math;

public class PrimeCheck {
    public static boolean isPrime(int n) {
        if (n <= 1) return false;
        for (int i = 2; i <= Math.sqrt(n); i++) {
            if (n % i == 0) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(isPrime(n));
        scanner.close();
    }
}
```

## Python Solution
```python
import math

def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(math.sqrt(n)) + 1):
        if n % i == 0:
            return False
    return True

n = int(input())
print(is_prime(n))

```

## JavaScript Solution
```javascript
function isPrime(n) {
  if (n <= 1) return false;
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i === 0) return false;
  }
  return true;
}

const n = parseInt(readline());
print(isPrime(n));
```