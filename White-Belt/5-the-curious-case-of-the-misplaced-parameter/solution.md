# Solutions for The Curious Case of the Misplaced Parameter

### Approach
The solution involves creating a function that accepts two integer arguments. Inside the function, we first print the value of the first argument 'a'. Then we calculate the sum of 'a' and 'b' and return the result. The main function handles reading input values from the console (using scanf or similar) passing them as arguments to the function, and finally printing the returned sum to the console.

## C Solution
```c
#include <stdio.h>

int sum_and_print(int a, int b) {
    printf("%d\n", a);
    return a + b;
}

int main() {
    int a, b;
    scanf("%d %d", &a, &b);
    int result = sum_and_print(a, b);
    printf("%d\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sum_and_print(int a, int b) {
    std::cout << a << std::endl;
    return a + b;
}

int main() {
    int a, b;
    std::cin >> a >> b;
    int result = sum_and_print(a, b);
    std::cout << result << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {
    public static int sumAndPrint(int a, int b) {
        System.out.println(a);
        return a + b;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        int result = sumAndPrint(a, b);
        System.out.println(result);
        scanner.close();
    }
}
```

## Python Solution
```python
def sum_and_print(a, b):
    print(a)
    return a + b

a, b = map(int, input().split())
result = sum_and_print(a, b)
print(result)
```

## JavaScript Solution
```javascript
function sumAndPrint(a, b) {
    console.log(a);
    return a + b;
}

const lines = require('fs').readFileSync('/dev/stdin').toString().split('\n');
const [a, b] = lines[0].split(' ').map(Number);
const result = sumAndPrint(a, b);
console.log(result);
```