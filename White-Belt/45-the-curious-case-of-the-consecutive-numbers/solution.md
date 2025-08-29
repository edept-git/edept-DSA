# Solutions for The Curious Case of the Consecutive Numbers

### Approach
The solution iterates through all possible pairs of the three input integers. For each pair, it checks if their sum is equal to the remaining integer using the addition (+) and equality (==) operators.  The time complexity is O(1) as it performs a fixed number of operations. The space complexity is O(1) as it uses a constant amount of extra space.

## C Solution
```c
#include <stdio.h>
int solve(int a, int b, int c) {
  if (a + b == c || a + c == b || b + c == a) {
    return 1;
  } else {
    return 0;
  }
}
int main() {
  int a, b, c;
scanf("%d %d %d", &a, &b, &c);
printf("%d\n", solve(a, b, c));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
using namespace std;
int solve(int a, int b, int c) {
  if (a + b == c || a + c == b || b + c == a) {
    return 1;
  } else {
    return 0;
  }
}
int main() {
  int a, b, c;
  cin >> a >> b >> c;
  cout << solve(a, b, c) << endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
public class Main {
  public static int solve(int a, int b, int c) {
    if (a + b == c || a + c == b || b + c == a) {
      return 1;
    } else {
      return 0;
    }
  }
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    int a = scanner.nextInt();
    int b = scanner.nextInt();
    int c = scanner.nextInt();
    System.out.println(solve(a, b, c));
    scanner.close();
  }
}
```

## Python Solution
```python
def solve(a, b, c):
  if a + b == c or a + c == b or b + c == a:
    return 1
  else:
    return 0
a, b, c = map(int, input().split())
print(solve(a, b, c))
```

## JavaScript Solution
```javascript
function solve(a, b, c) {
  if (a + b === c || a + c === b || b + c === a) {
    return 1;
  } else {
    return 0;
  }
}
const input = require('readline-sync').question().split(' ').map(Number);
const [a, b, c] = input;
console.log(solve(a, b, c));
```