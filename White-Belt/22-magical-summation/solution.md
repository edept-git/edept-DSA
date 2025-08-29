# Solutions for Magical Summation

### Approach
The approach is straightforward. We use the arithmetic operator '+' to calculate the sum of the three input integers.  Then, we employ a relational operator '>' to check if the sum is greater than 100. Based on the result of this comparison, we use a conditional statement (if-else) to return either the sum or -1.  The time complexity is O(1) as we perform a constant number of operations, and the space complexity is also O(1) as we use a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int magicalSum(int a, int b, int c) {
    int sum = a + b + c;
    if (sum > 100) {
        return sum;
    } else {
        return -1;
    }
}

int main() {
    int a, b, c;
    scanf("%d %d %d", &a, &b, &c);
    printf("%d\n", magicalSum(a, b, c));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int magicalSum(int a, int b, int c) {
    int sum = a + b + c;
    if (sum > 100) {
        return sum;
    } else {
        return -1;
    }
}

int main() {
    int a, b, c;
    std::cin >> a >> b >> c;
    std::cout << magicalSum(a, b, c) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class MagicalSum {
    public static int magicalSum(int a, int b, int c) {
        int sum = a + b + c;
        if (sum > 100) {
            return sum;
        } else {
            return -1;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        int c = scanner.nextInt();
        System.out.println(magicalSum(a, b, c));
        scanner.close();
    }
}
```

## Python Solution
```python
def magicalSum(a, b, c):
    sum = a + b + c
    if sum > 100:
        return sum
    else:
        return -1

a, b, c = map(int, input().split())
print(magicalSum(a, b, c))
```

## JavaScript Solution
```javascript
function magicalSum(a, b, c) {
    let sum = a + b + c;
    if (sum > 100) {
        return sum;
    } else {
        return -1;
    }
}

const input = require('readline-sync').question().split(' ').map(Number);
const a = input[0];
const b = input[1];
const c = input[2];
console.log(magicalSum(a,b,c));
```