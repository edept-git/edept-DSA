# Solutions for Number Sign Detector

### Approach
The problem requires us to classify an integer based on its sign. We can achieve this using a series of conditional checks. First, we read the integer input from the user. Then, we use an `if` statement to check if the number is greater than zero. If it is, the number is positive. If not, we proceed to an `else if` statement to check if the number is less than zero. If this condition is met, the number is negative. Finally, if neither of the previous conditions is true, it implies that the number must be exactly zero, so we use an `else` block to handle this case. The appropriate classification ("Positive", "Negative", or "Zero") is then printed.

This approach involves a constant number of comparisons regardless of the input value, making its **time complexity** O(1). We only store the input number and a few temporary variables, resulting in a **space complexity** of O(1).

## C Solution
```c
#include <stdio.h>

// Function to detect the sign of a number
const char* detectSign(int num) {
    if (num > 0) {
        return "Positive";
    } else if (num < 0) {
        return "Negative";
    } else {
        return "Zero";
    }
}

int main() {
    int num;
    // Read input
    scanf("%d", &num);
    
    // Call the function and print the result
    printf("%s\n", detectSign(num));
    
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Function to detect the sign of a number
std::string detectSign(int num) {
    if (num > 0) {
        return "Positive";
    } else if (num < 0) {
        return "Negative";
    } else {
        return "Zero";
    }
}

int main() {
    int num;
    // Read input
    std::cin >> num;
    
    // Call the function and print the result
    std::cout << detectSign(num) << std::endl;
    
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to detect the sign of a number
    public String detectSign(int num) {
        if (num > 0) {
            return "Positive";
        } else if (num < 0) {
            return "Negative";
        } else {
            return "Zero";
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Read input
        int num = scanner.nextInt();
        scanner.close();
        
        // Create an instance of Solution and call the function
        Solution sol = new Solution();
        System.out.println(sol.detectSign(num));
    }
}
```

## Python Solution
```python
def detect_sign(num: int) -> str:
    """
    Detects the sign of an integer.

    Args:
        num: The integer to check.

    Returns:
        A string indicating "Positive", "Negative", or "Zero".
    """
    if num > 0:
        return "Positive"
    elif num < 0:
        return "Negative"
    else:
        return "Zero"

if __name__ == "__main__":
    # Read input
    num_str = input()
    num = int(num_str)
    
    # Call the function and print the result
    print(detect_sign(num))
```

## JavaScript Solution
```javascript
// Function to detect the sign of a number
function detectSign(num) {
    if (num > 0) {
        return "Positive";
    } else if (num < 0) {
        return "Negative";
    } else {
        return "Zero";
    }
}

// Read input from stdin
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    const num = parseInt(line, 10);
    // Call the function and print the result
    console.log(detectSign(num));
    rl.close();
});
```