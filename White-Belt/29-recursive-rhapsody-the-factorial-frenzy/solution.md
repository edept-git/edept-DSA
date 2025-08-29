# Solutions for Recursive Rhapsody: The Factorial Frenzy

### Approach
The solution uses a recursive approach. The factorial function calls itself with a smaller input until it reaches the base case (n=0 or n=1, where the factorial is 1). The recursive step involves multiplying the current number with the factorial of the number minus one. The time complexity is O(n) due to the recursive calls, and the space complexity is O(n) due to the recursive call stack.

## C Solution
```c
#include <stdio.h>

long long factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

int main() {
    int n;
    scanf("%d", &n);
    printf("%lld\n", factorial(n));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

long long factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

int main() {
    int n;
    std::cin >> n;
    std::cout << factorial(n) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.*;

public class Factorial {
    public static long factorial(int n) {
        if (n == 0 || n == 1) {
            return 1;
        } else {
            return n * factorial(n - 1);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(factorial(n));
        scanner.close();
    }
}
```

## Python Solution
```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * factorial(n - 1)

n = int(input())
print(factorial(n))
```

## JavaScript Solution
```javascript
function factorial(n) {
  if (n === 0 || n === 1) {
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}

const n = parseInt(process.argv[2]);
console.log(factorial(n));
```