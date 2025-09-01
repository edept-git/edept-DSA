# Solutions for Recursive Power Play

### Approach
The recursive approach involves breaking down the problem into smaller subproblems.  For positive exponents, xⁿ = x * xⁿ⁻¹. For negative exponents, x⁻ⁿ = 1 / xⁿ. The base cases are n = 0 (result is 1) and n = 1 (result is x).  The time complexity is O(n) due to the recursive calls. The space complexity is O(n) in the worst case due to the recursive call stack.

## C Solution
```c
#include <stdio.h>
double power(double x, int n) {
    if (n == 0) return 1;
    if (n == 1) return x;
    if (n < 0) return 1.0 / power(x, -n);
    return x * power(x, n - 1);
}
int main() {
    double x; int n; 
    scanf("%lf %d", &x, &n);
    printf("%.2lf\n", power(x, n));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <iomanip>
double power(double x, int n) {
    if (n == 0) return 1;
    if (n == 1) return x;
    if (n < 0) return 1.0 / power(x, -n);
    return x * power(x, n - 1);
}
int main() {
    double x; int n; 
    std::cin >> x >> n;
    std::cout << std::fixed << std::setprecision(2) << power(x, n) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
public class RecursivePower {
    public static double power(double x, int n) {
        if (n == 0) return 1;
        if (n == 1) return x;
        if (n < 0) return 1.0 / power(x, -n);
        return x * power(x, n - 1);
    }
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        double x = input.nextDouble();
        int n = input.nextInt();
        System.out.printf("%.2f\n", power(x, n));
        input.close();
    }
}
```

## Python Solution
```python
def power(x, n):
    if n == 0:
        return 1
    if n == 1:
        return x
    if n < 0:
        return 1.0 / power(x, -n)
    return x * power(x, n - 1)

x, n = map(float, input().split())
n = int(n)
print(f"{power(x, n):.2f}")
```

## JavaScript Solution
```javascript
function power(x, n) {
    if (n === 0) return 1;
    if (n === 1) return x;
    if (n < 0) return 1.0 / power(x, -n);
    return x * power(x, n - 1);
}
const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim().split(' ');
const x = parseFloat(input[0]);
const n = parseInt(input[1]);
console.log(power(x, n).toFixed(2));
```