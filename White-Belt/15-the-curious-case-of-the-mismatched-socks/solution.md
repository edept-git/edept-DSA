# Solutions for The Curious Case of the Mismatched Socks

### Approach
This problem involves a simple function that takes two integer arguments representing the number of red and blue socks. It adds these two numbers together to calculate the total number of socks. The time complexity is O(1) as it involves only a single addition operation. The space complexity is also O(1) as it uses only a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int count_socks(int red_socks, int blue_socks) {
  return red_socks + blue_socks;
}

int main() {
  int red, blue;
  scanf("%d %d", &red, &blue);
  printf("%d\n", count_socks(red, blue));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int count_socks(int red_socks, int blue_socks) {
  return red_socks + blue_socks;
}

int main() {
  int red, blue;
  std::cin >> red >> blue;
  std::cout << count_socks(red, blue) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class SockCounter {

    public static int countSocks(int redSocks, int blueSocks) {
        return redSocks + blueSocks;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int red = scanner.nextInt();
        int blue = scanner.nextInt();
        System.out.println(countSocks(red, blue));
        scanner.close();
    }
}
```

## Python Solution
```python
def count_socks(red_socks, blue_socks):
  return red_socks + blue_socks

red, blue = map(int, input().split())
print(count_socks(red, blue))
```

## JavaScript Solution
```javascript
function countSocks(redSocks, blueSocks) {
  return redSocks + blueSocks;
}

const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim().split(' ')
const red = parseInt(input[0]);
const blue = parseInt(input[1]);
console.log(countSocks(red, blue));
```