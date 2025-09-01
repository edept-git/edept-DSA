# Solutions for EvenSum Explorer

### Approach
The most straightforward approach to solve this problem is to use a loop. We can initialize a variable, `sum`, to 0. Then, we iterate through numbers starting from 1 up to `N` (inclusive) using either a `for` or `while` loop. Inside the loop, for each number, we check if it is an even number. A number is even if it is perfectly divisible by 2, which can be checked using the modulus operator (`%`). If `number % 2 == 0`, then the number is even. If the number is even, we add it to our `sum` variable. After the loop completes, the `sum` variable will hold the total sum of all even numbers up to `N`, which is then returned. This approach involves a single pass from 1 to `N`, so the time complexity is O(N). The space complexity is O(1) as we only use a few constant extra variables to store the sum, loop counter, and input `N`.

## C Solution
```c
#include <stdio.h>

// Function to calculate the sum of even numbers up to N
int sumEvenNumbers(int n) {
    int sum = 0;
    for (int i = 1; i <= n; i++) {
        if (i % 2 == 0) {
            sum += i;
        }
    }
    return sum;
}

int main() {
    int n;
    // Read input from stdin
    if (scanf("%d", &n) != 1) {
        // Handle potential input error
        return 1;
    }

    // Call the logic function
    int result = sumEvenNumbers(n);

    // Print the result to stdout
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate the sum of even numbers up to N
int sumEvenNumbers(int n) {
    int sum = 0;
    for (int i = 1; i <= n; ++i) {
        if (i % 2 == 0) {
            sum += i;
        }
    }
    return sum;
}

int main() {
    int n;
    // Read input from stdin
    std::cin >> n;

    // Call the logic function
    int result = sumEvenNumbers(n);

    // Print the result to stdout
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate the sum of even numbers up to N
    public static int sumEvenNumbers(int n) {
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            if (i % 2 == 0) {
                sum += i;
            }
        }
        return sum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Read input from stdin
        int n = scanner.nextInt();
        scanner.close(); // Close the scanner to release resources

        // Call the logic function
        int result = sumEvenNumbers(n);

        // Print the result to stdout
        System.out.println(result);
    }
}
```

## Python Solution
```python
def sum_even_numbers(n):
    """Calculates the sum of even numbers up to N."""
    total_sum = 0
    for i in range(1, n + 1):
        if i % 2 == 0:
            total_sum += i
    return total_sum

if __name__ == "__main__":
    # Read input from stdin
    n = int(input())

    # Call the logic function
    result = sum_even_numbers(n);

    # Print the result to stdout
    print(result)
```

## JavaScript Solution
```javascript
function sumEvenNumbers(n) {
    let sum = 0;
    for (let i = 1; i <= n; i++) {
        if (i % 2 === 0) {
            sum += i;
        }
    }
    return sum;
}

// To run in a typical competitive programming environment (Node.js)
// Read input from stdin
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const n = parseInt(line.trim(), 10);
    // Call the logic function
    const result = sumEvenNumbers(n);
    // Print the result to stdout
    console.log(result);
    rl.close(); // Close the readline interface after processing input
});

```