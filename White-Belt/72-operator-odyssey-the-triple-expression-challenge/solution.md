# Solutions for Operator Odyssey: The Triple Expression Challenge

### Approach
The problem requires direct application of arithmetic, relational, and logical operators. We will read three integer inputs. First, we compute the arithmetic expression `(num1 + num2) * num3` using addition and multiplication. Next, we evaluate the logical expression `(num1 > num2) && (num2 < num3)`. This involves two relational comparisons (`num1 > num2` and `num2 < num3`) which yield boolean results, followed by a logical AND operation (`&&`) on these two boolean results. The results are then printed to standard output. No complex data structures are required beyond primitive integer and boolean types. The time complexity for this approach is O(1) because it involves a fixed number of arithmetic and logical operations, independent of the input values' magnitude (within standard integer limits). The space complexity is also O(1) as only a few variables are used to store inputs and intermediate results.

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>

void evaluateExpressions(int num1, int num2, int num3) {
    // Arithmetic Calculation
    int arithmeticResult = (num1 + num2) * num3;
    printf("%d\n", arithmeticResult);

    // Logical Calculation
    bool logicalResult = (num1 > num2) && (num2 < num3);
    if (logicalResult) {
        printf("true\n");
    } else {
        printf("false\n");
    }
}

int main() {
    int n1, n2, n3;
    if (scanf("%d", &n1) != 1) return 1;
    if (scanf("%d", &n2) != 1) return 1;
    if (scanf("%d", &n3) != 1) return 1;

    evaluateExpressions(n1, n2, n3);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

void evaluateExpressions(int num1, int num2, int num3) {
    // Arithmetic Calculation
    int arithmeticResult = (num1 + num2) * num3;
    std::cout << arithmeticResult << std::endl;

    // Logical Calculation
    bool logicalResult = (num1 > num2) && (num2 < num3);
    std::cout << std::boolalpha << logicalResult << std::endl;
}

int main() {
    int n1, n2, n3;
    if (!(std::cin >> n1)) return 1;
    if (!(std::cin >> n2)) return 1;
    if (!(std::cin >> n3)) return 1;

    evaluateExpressions(n1, n2, n3);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    public static void evaluateExpressions(int num1, int num2, int num3) {
        // Arithmetic Calculation
        int arithmeticResult = (num1 + num2) * num3;
        System.out.println(arithmeticResult);

        // Logical Calculation
        boolean logicalResult = (num1 > num2) && (num2 < num3);
        System.out.println(logicalResult);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n1 = scanner.nextInt();
        int n2 = scanner.nextInt();
        int n3 = scanner.nextInt();
        scanner.close();

        evaluateExpressions(n1, n2, n3);
    }
}
```

## Python Solution
```python
def evaluate_expressions(num1, num2, num3):
    # Arithmetic Calculation
    arithmetic_result = (num1 + num2) * num3
    print(arithmetic_result)

    # Logical Calculation
    logical_result = (num1 > num2) and (num2 < num3)
    print(logical_result)

if __name__ == "__main__":
    n1 = int(input())
    n2 = int(input())
    n3 = int(input())

    evaluate_expressions(n1, n2, n3)

```

## JavaScript Solution
```javascript
function evaluateExpressions(num1, num2, num3) {
    // Arithmetic Calculation
    const arithmeticResult = (num1 + num2) * num3;
    console.log(arithmeticResult);

    // Logical Calculation
    const logicalResult = (num1 > num2) && (num2 < num3);
    console.log(logicalResult);
}

// Read input from stdin
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(parseInt(line, 10));
});

rl.on('close', () => {
    const n1 = inputLines[0];
    const n2 = inputLines[1];
    const n3 = inputLines[2];
    evaluateExpressions(n1, n2, n3);
});

```