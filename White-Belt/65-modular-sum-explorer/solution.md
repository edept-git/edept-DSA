# Solutions for Modular Sum Explorer

### Approach
The problem asks for the result of `(a + b) % m`. The most direct and efficient approach is to first compute the sum of the two integers, `a` and `b`. Let's call this sum `S = a + b`. After obtaining `S`, the next step is to apply the modulo operator with `m` to `S`. The final answer will be `S % m`. This approach relies on the fundamental definition of the modulo operator, which gives the remainder of a division. Since only a fixed number of arithmetic operations (one addition and one modulo) are performed, the time complexity of this algorithm is O(1). Similarly, because we only need to store a few variables (inputs `a`, `b`, `m`, and the intermediate sum `S`), the space complexity is also O(1). The integer types used in most languages (like `int` in C++/Java) can typically hold values up to `2 * 10^9`, which is sufficient for `a + b` given the constraints `a, b <= 10^9`.

## C Solution
```c
#include <stdio.h>

// Function to calculate (a + b) % m
int calculateModularSum(int a, int b, int m) {
    int sum = a + b;
    return sum % m;
}

int main() {
    int a, b, m;

    // Read input values
    if (scanf("%d", &a) != 1) return 1;
    if (scanf("%d", &b) != 1) return 1;
    if (scanf("%d", &m) != 1) return 1;

    // Calculate and print the result
    int result = calculateModularSum(a, b, m);
    printf("%d\n", result);

    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate (a + b) % m
int calculateModularSum(int a, int b, int m) {
    int sum = a + b;
    return sum % m;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int a, b, m;

    // Read input values
    std::cin >> a >> b >> m;

    // Calculate and print the result
    int result = calculateModularSum(a, b, m);
    std::cout << result << std::endl;

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate (a + b) % m
    public static int calculateModularSum(int a, int b, int m) {
        int sum = a + b;
        return sum % m;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read input values
        int a = scanner.nextInt();
        int b = scanner.nextInt();
        int m = scanner.nextInt();

        // Calculate and print the result
        int result = calculateModularSum(a, b, m);
        System.out.println(result);

        scanner.close();
    }
}

```

## Python Solution
```python
def calculate_modular_sum(a, b, m):
    """
    Calculates (a + b) % m.
    """
    sum_val = a + b
    return sum_val % m

if __name__ == "__main__":
    # Read input values
    a = int(input())
    b = int(input())
    m = int(input())

    # Calculate and print the result
    result = calculate_modular_sum(a, b, m)
    print(result)

```

## JavaScript Solution
```javascript
function calculateModularSum(a, b, m) {
    // Function to calculate (a + b) % m
    let sum = a + b;
    return sum % m;
}

// Read input from stdin
let input = '';
process.stdin.on('data', chunk => {
    input += chunk;
});

process.stdin.on('end', () => {
    const lines = input.trim().split('\n');
    const a = parseInt(lines[0], 10);
    const b = parseInt(lines[1], 10);
    const m = parseInt(lines[2], 10);

    // Calculate and print the result
    const result = calculateModularSum(a, b, m);
    console.log(result);
});

```