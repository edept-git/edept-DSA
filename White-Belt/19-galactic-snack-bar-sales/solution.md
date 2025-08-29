# Solutions for Galactic Snack Bar Sales

### Approach
The solution involves declaring integer variables to store the number of each snack type sold.  These variables are then added together to compute the total number of snacks sold.  The time complexity is O(1) as it involves a fixed number of arithmetic operations. The space complexity is O(1) as it uses a constant amount of memory regardless of the input values.

## C Solution
```c
#include <stdio.h>

int calculateTotalSnacks(int fizzbangs, int zapZaps, int glimmerglobs) {
    return fizzbangs + zapZaps + glimmerglobs;
}

int main() {
    int fizzbangs, zapZaps, glimmerglobs;
    scanf("%d %d %d", &fizzbangs, &zapZaps, &glimmerglobs);
    printf("%d\n", calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int calculateTotalSnacks(int fizzbangs, int zapZaps, int glimmerglobs) {
    return fizzbangs + zapZaps + glimmerglobs;
}

int main() {
    int fizzbangs, zapZaps, glimmerglobs;
    std::cin >> fizzbangs >> zapZaps >> glimmerglobs;
    std::cout << calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class SnackBar {
    public static int calculateTotalSnacks(int fizzbangs, int zapZaps, int glimmerglobs) {
        return fizzbangs + zapZaps + glimmerglobs;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int fizzbangs = scanner.nextInt();
        int zapZaps = scanner.nextInt();
        int glimmerglobs = scanner.nextInt();
        System.out.println(calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs));
        scanner.close();
    }
}
```

## Python Solution
```python
def calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs):
    return fizzbangs + zapZaps + glimmerglobs

fizzbangs, zapZaps, glimmerglobs = map(int, input().split())
print(calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs))
```

## JavaScript Solution
```javascript
function calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs) {
  return fizzbangs + zapZaps + glimmerglobs;
}

const input = require('readline-sync').question().split(' ');
const fizzbangs = parseInt(input[0]);
const zapZaps = parseInt(input[1]);
const glimmerglobs = parseInt(input[2]);
console.log(calculateTotalSnacks(fizzbangs, zapZaps, glimmerglobs));
```