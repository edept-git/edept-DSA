# Solutions for The Summing Spree

### Approach
The solution uses a `for` loop to iterate through numbers from 1 to N. Inside the loop, an `if` condition checks if the number is even. If it is, the number is added to a `sum` variable.  The time complexity is O(N) because we iterate through N numbers. The space complexity is O(1) because we only use a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int sumEvenNumbers(int n) {
  int sum = 0;
  for (int i = 1; i <= n; i++) {
    if (i % 2 == 0) {
      sum += i;
    }
  }
  return sum;
}

int main() {
  int n;
  scanf("%d", &n);
  printf("%d\n", sumEvenNumbers(n));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sumEvenNumbers(int n) {
  int sum = 0;
  for (int i = 2; i <= n; i += 2) {
    sum += i;
  }
  return sum;
}

int main() {
  int n;
  std::cin >> n;
  std::cout << sumEvenNumbers(n) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class SumEven {
    public static int sumEvenNumbers(int n) {
        int sum = 0;
        for (int i = 2; i <= n; i += 2) {
            sum += i;
        }
        return sum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(sumEvenNumbers(n));
        scanner.close();
    }
}
```

## Python Solution
```python
def sum_even_numbers(n):
  sum = 0
  for i in range(2, n + 1, 2):
    sum += i
  return sum

n = int(input())
print(sum_even_numbers(n))
```

## JavaScript Solution
```javascript
function sumEvenNumbers(n) {
  let sum = 0;
  for (let i = 2; i <= n; i += 2) {
    sum += i;
  }
  return sum;
}

const n = parseInt(process.argv[2]);
console.log(sumEvenNumbers(n));
```