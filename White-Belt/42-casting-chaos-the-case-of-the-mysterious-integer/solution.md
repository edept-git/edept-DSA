# Solutions for Casting Chaos: The Case of the Mysterious Integer

### Approach
The algorithm involves a sequence of explicit type castings.  First, the integer `n` is cast to a double, increasing its precision. Then, it's cast to a float, potentially reducing precision depending on the float's size. Finally, it's cast back to an integer, truncating any fractional part. The time complexity is O(1) as it involves only constant-time operations. The space complexity is also O(1) as it uses only a few variables.

## C Solution
```c
#include <stdio.h>

int cast_integer(int n) {
    double double_n = (double)n;
    float float_n = (float)double_n;
    int final_n = (int)float_n;
    return final_n;
}

int main() {
    int n;
    scanf("%d", &n);
    printf("%d\n", cast_integer(n));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int cast_integer(int n) {
    double double_n = static_cast<double>(n);
    float float_n = static_cast<float>(double_n);
    int final_n = static_cast<int>(float_n);
    return final_n;
}

int main() {
    int n;
    std::cin >> n;
    std::cout << cast_integer(n) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class CastingChaos {
    public static int castInteger(int n) {
        double doubleN = (double) n;
        float floatN = (float) doubleN;
        int finalN = (int) floatN;
        return finalN;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(castInteger(n));
        scanner.close();
    }
}
```

## Python Solution
```python
def cast_integer(n):
    double_n = float(n)
    float_n = float(double_n)
    final_n = int(float_n)
    return final_n

n = int(input())
print(cast_integer(n))
```

## JavaScript Solution
```javascript
function castInteger(n) {
  let doubleN = parseFloat(n);
  let floatN = parseFloat(doubleN);
  let finalN = parseInt(floatN);
  return finalN;
}

let n = parseInt(readline());
print(castInteger(n));
```