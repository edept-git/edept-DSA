# Solutions for Recursive Factorial Frenzy

### Approach
The solution uses a recursive approach.  The function `factorial` takes an integer `n` as input. The base case is when `n` is 0, in which case it returns 1 (0! = 1). Otherwise, it recursively calls itself with `n-1` and multiplies the result by `n`. This continues until the base case is reached. The time complexity is O(n) due to the recursive calls, and the space complexity is O(n) due to the recursive call stack.

## C Solution
```c
#include <stdio.h>

long long factorial(int n) {
    if (n == 0) {
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
    if (n == 0) {
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
        if (n == 0) {
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
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)

n = int(input())
print(factorial(n))
```

## JavaScript Solution
```javascript
function factorial(n) {
  if (n === 0) {
    return 1;
  } else {
    return n * factorial(n - 1);
  }
}

const n = parseInt(process.argv[2]);
console.log(factorial(n));
```