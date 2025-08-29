# Solutions for Sum of Even Numbers in a Range

### Approach
The solution uses a `for` loop to iterate through the given range. Inside the loop, an `if` condition checks if the current number is even. If it's even, it's added to a running sum.  The time complexity is O(n), where n is the range size, and space complexity is O(1) as we only use a few variables.

## C Solution
```c
#include <stdio.h>

int sumEvenInRange(int start, int end) {
  int sum = 0;
  for (int i = start; i <= end; i++) {
    if (i % 2 == 0) {
      sum += i;
    }
  }
  return sum;
}

int main() {
  int start, end;
  scanf("%d %d", &start, &end);
  int result = sumEvenInRange(start, end);
  printf("%d\n", result);
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sumEvenInRange(int start, int end) {
  int sum = 0;
  for (int i = start; i <= end; i++) {
    if (i % 2 == 0) {
      sum += i;
    }
  }
  return sum;
}

int main() {
  int start, end;
  std::cin >> start >> end;
  int result = sumEvenInRange(start, end);
  std::cout << result << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class SumEven {

  public static int sumEvenInRange(int start, int end) {
    int sum = 0;
    for (int i = start; i <= end; i++) {
      if (i % 2 == 0) {
        sum += i;
      }
    }
    return sum;
  }

  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    int start = scanner.nextInt();
    int end = scanner.nextInt();
    int result = sumEvenInRange(start, end);
    System.out.println(result);
    scanner.close();
  }
}
```

## Python Solution
```python
def sum_even_in_range(start, end):
  sum = 0
  for i in range(start, end + 1):
    if i % 2 == 0:
      sum += i
  return sum

start, end = map(int, input().split())
result = sum_even_in_range(start, end)
print(result)
```

## JavaScript Solution
```javascript
function sumEvenInRange(start, end) {
  let sum = 0;
  for (let i = start; i <= end; i++) {
    if (i % 2 === 0) {
      sum += i;
    }
  }
  return sum;
}

const input = require('readline-sync').question().split(' ').map(Number);
const start = input[0];
const end = input[1];
const result = sumEvenInRange(start, end);
console.log(result);
```