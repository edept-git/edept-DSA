# Solutions for Counting Sheep: A Time Complexity Tale

### Approach
The most straightforward approach is to use a simple loop to iterate from 1 to `n`, summing the numbers along the way.  This approach has a time complexity of O(n) because the number of operations is directly proportional to the input `n`. The space complexity is O(1) because we only use a constant amount of extra space regardless of the input size.

## C Solution
```c
#include <stdio.h>

long long countSheep(long long n) {
  long long sum = 0;
  for (long long i = 1; i <= n; i++) {
    sum += i;
  }
  return sum;
}

int main() {
  long long n;
  scanf("%lld", &n);
  printf("%lld\n", countSheep(n));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

long long countSheep(long long n) {
  long long sum = 0;
  for (long long i = 1; i <= n; i++) {
    sum += i;
  }
  return sum;
}

int main() {
  long long n;
  std::cin >> n;
  std::cout << countSheep(n) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class CountSheep {

    public static long countSheep(long n) {
        long sum = 0;
        for (long i = 1; i <= n; i++) {
            sum += i;
        }
        return sum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        long n = scanner.nextLong();
        System.out.println(countSheep(n));
        scanner.close();
    }
}
```

## Python Solution
```python
def count_sheep(n):
  sum = 0
  for i in range(1, n + 1):
    sum += i
  return sum

n = int(input())
print(count_sheep(n))
```

## JavaScript Solution
```javascript
function countSheep(n) {
  let sum = 0;
  for (let i = 1; i <= n; i++) {
    sum += i;
  }
  return sum;
}

const n = parseInt(process.argv[2]);
console.log(countSheep(n));
```