# Solutions for Numeric Ascent: Summing Your Way Up

### Approach
The problem asks us to find the sum of all integers from 1 to a given positive integer `N`. A straightforward way to solve this is to use a loop. We can initialize a variable, say `totalSum`, to 0. Then, we start a loop that iterates from 1 up to `N`. In each iteration, we add the current loop variable's value to `totalSum`. After the loop finishes, `totalSum` will hold the desired sum.

For example, if `N=3`:
1. `totalSum = 0`
2. Loop `i = 1`: `totalSum = 0 + 1 = 1`
3. Loop `i = 2`: `totalSum = 1 + 2 = 3`
4. Loop `i = 3`: `totalSum = 3 + 3 = 6`
The loop finishes, and `totalSum` is 6.

**Time Complexity:** The loop runs `N` times, performing a constant amount of work (an addition and an assignment) in each iteration. Therefore, the total time complexity is proportional to `N`, which is written as **O(N)**. This means if `N` doubles, the time taken approximately doubles.

**Space Complexity:** We only use a few variables (`N`, `totalSum`, and the loop counter `i`). The amount of memory used does not grow with the input `N`. Hence, the space complexity is **O(1)** (constant space).

## C Solution
```c
#include <stdio.h>

int calculateSum(int n) {
    int totalSum = 0;
    for (int i = 1; i <= n; i++) {
        totalSum += i;
    }
    return totalSum;
}

int main() {
    int n;
    // Read input from stdin
    scanf("%d", &n);

    // Call the core logic function
    int result = calculateSum(n);

    // Print output to stdout
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int calculateSum(int n) {
    int totalSum = 0;
    for (int i = 1; i <= n; i++) {
        totalSum += i;
    }
    return totalSum;
}

int main() {
    int n;
    // Read input from stdin
    std::cin >> n;

    // Call the core logic function
    int result = calculateSum(n);

    // Print output to stdout
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    public static int calculateSum(int n) {
        int totalSum = 0;
        for (int i = 1; i <= n; i++) {
            totalSum += i;
        }
        return totalSum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Read input from stdin
        int n = scanner.nextInt();
        scanner.close();

        // Call the core logic function
        int result = calculateSum(n);

        // Print output to stdout
        System.out.println(result);
    }
}
```

## Python Solution
```python
def calculateSum(n: int) -> int:
    total_sum = 0
    for i in range(1, n + 1):
        total_sum += i
    return total_sum

if __name__ == "__main__":
    # Read input from stdin
    n = int(input())

    # Call the core logic function
    result = calculateSum(n)

    # Print output to stdout
    print(result)
```

## JavaScript Solution
```javascript
function calculateSum(n) {
    let totalSum = 0;
    for (let i = 1; i <= n; i++) {
        totalSum += i;
    }
    return totalSum;
}

// Read input from stdin
// For competitive programming, input is typically read line by line or all at once.
// This example assumes a single integer input on the first line.
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const n = parseInt(line.trim(), 10);

    // Call the core logic function
    const result = calculateSum(n);

    // Print output to stdout
    console.log(result);

    rl.close();
});
```