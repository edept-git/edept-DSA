# Solutions for The Nearest Multiple

### Approach
The problem asks us to find the smallest integer `X` that is greater than or equal to `N` and perfectly divisible by `K`. We can achieve this efficiently using the modulo operator.

First, we calculate the remainder when `N` is divided by `K`. Let this be `remainder = N % K`.

There are two main cases:
1.  If `remainder` is 0: This means `N` is already perfectly divisible by `K`. In this case, `N` itself is the smallest number that satisfies the conditions, so `X = N`.
2.  If `remainder` is not 0: This means `N` is not perfectly divisible by `K`. To find the next multiple of `K` that is greater than or equal to `N`, we need to determine how much more we need to add to `N` to reach the next multiple. Since `N` is `remainder` units past a multiple of `K`, we need to add `K - remainder` to `N`. For example, if `N = 10` and `K = 3`, `remainder = 10 % 3 = 1`. We need to add `3 - 1 = 2` to `N`, resulting in `10 + 2 = 12`. This `12` is the next multiple of 3. So, `X = N + (K - remainder)`.

This algorithm uses basic arithmetic operations and the modulo operator. No complex data structures are required.

**Time Complexity:** O(1) because it involves a few constant-time arithmetic operations.
**Space Complexity:** O(1) as it only uses a few variables to store numbers.

## C Solution
```c
#include <stdio.h>

// Function to find the nearest multiple
int findNearestMultiple(int n, int k) {
    // Constraints state 1 <= K <= 100, so k will never be 0.
    int remainder = n % k;
    if (remainder == 0) {
        return n;
    } else {
        return n + (k - remainder);
    }
}

int main() {
    int n, k;
    // Assuming N and K are provided on separate lines or space-separated on one line
    if (scanf("%d %d", &n, &k) != 2) {
        // Handle potential input error
        return 1; 
    }
    int result = findNearestMultiple(n, k);
    printf("%d\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to find the nearest multiple
int findNearestMultiple(int n, int k) {
    // Constraints state 1 <= K <= 100, so k will never be 0.
    int remainder = n % k;
    if (remainder == 0) {
        return n;
    } else {
        return n + (k - remainder);
    }
}

int main() {
    int n, k;
    std::cin >> n >> k;
    int result = findNearestMultiple(n, k);
    std::cout << result << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to find the nearest multiple
    public static int findNearestMultiple(int n, int k) {
        // Constraints state 1 <= K <= 100, so k will never be 0.
        int remainder = n % k;
        if (remainder == 0) {
            return n;
        } else {
            return n + (k - remainder);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int k = scanner.nextInt();
        int result = findNearestMultiple(n, k);
        System.out.println(result);
        scanner.close();
    }
}
```

## Python Solution
```python
def find_nearest_multiple(n, k):
    # Constraints state 1 <= K <= 100, so k will never be 0.
    remainder = n % k
    if remainder == 0:
        return n
    else:
        return n + (k - remainder)

def main():
    # Assuming N and K are provided on separate lines
    n = int(input())
    k = int(input())
    result = find_nearest_multiple(n, k)
    print(result)

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Function to find the nearest multiple
function findNearestMultiple(n, k) {
    // Constraints state 1 <= K <= 100, so k will never be 0.
    let remainder = n % k;
    if (remainder === 0) {
        return n;
    } else {
        return n + (k - remainder);
    }
}

// Main function to handle input/output
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let inputLines = [];
    rl.on('line', (line) => {
        inputLines.push(line);
    }).on('close', () => {
        const n = parseInt(inputLines[0]);
        const k = parseInt(inputLines[1]);
        const result = findNearestMultiple(n, k);
        console.log(result);
    });
}

main();
```