# Solutions for Bit Flipper Challenge

### Approach
The problem asks us to flip a specific bit (the `n`-th bit) in a given integer `num`. To do this, we can utilize the properties of bitwise operators. The key is to create a 'mask' where only the `n`-th bit is set to 1, and all other bits are 0. This mask can be created by left-shifting the integer `1` by `n` positions (`1 << n`). For example, if `n=1`, `1 << 1` results in `...0010`. If `n=2`, `1 << 2` results in `...0100`. Once we have this mask, we can use the bitwise XOR (`^`) operator. XORing a bit with 1 flips its value (0 becomes 1, 1 becomes 0), while XORing a bit with 0 leaves it unchanged. Therefore, `num ^ (1 << n)` will flip only the `n`-th bit of `num` and leave all other bits as they were. This approach involves a constant number of bitwise operations, resulting in a **Time Complexity** of O(1) and **Space Complexity** of O(1).

## C Solution
```c
#include <stdio.h>

// Function to toggle the n-th bit of a number
int toggleNthBit(int num, int n) {
    // Create a mask with only the n-th bit set to 1
    int mask = 1 << n;
    // XOR num with the mask to toggle the n-th bit
    return num ^ mask;
}

int main() {
    int num, n;
    // Read input values
    if (scanf("%d %d", &num, &n) != 2) {
        return 1; // Error reading input
    }

    // Call the logic function
    int result = toggleNthBit(num, n);

    // Print the result
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to toggle the n-th bit of a number
int toggleNthBit(int num, int n) {
    // Create a mask with only the n-th bit set to 1
    int mask = 1 << n;
    // XOR num with the mask to toggle the n-th bit
    return num ^ mask;
}

int main() {
    int num, n;
    // Read input values
    std::cin >> num >> n;

    // Call the logic function
    int result = toggleNthBit(num, n);

    // Print the result
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to toggle the n-th bit of a number
    public static int toggleNthBit(int num, int n) {
        // Create a mask with only the n-th bit set to 1
        int mask = 1 << n;
        // XOR num with the mask to toggle the n-th bit
        return num ^ mask;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read input values
        int num = scanner.nextInt();
        int n = scanner.nextInt();

        // Call the logic function
        int result = toggleNthBit(num, n);

        // Print the result
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def toggle_nth_bit(num: int, n: int) -> int:
    # Create a mask with only the n-th bit set to 1
    mask = 1 << n
    # XOR num with the mask to toggle the n-th bit
    return num ^ mask

if __name__ == '__main__':
    # Read input values
    num, n = map(int, input().split())

    # Call the logic function
    result = toggle_nth_bit(num, n)

    # Print the result
    print(result)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to toggle the n-th bit of a number
function toggleNthBit(num, n) {
    // Create a mask with only the n-th bit set to 1
    let mask = 1 << n;
    // XOR num with the mask to toggle the n-th bit
    return num ^ mask;
}

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    // Assuming input is space-separated numbers on one line
    const [num, n] = inputLines[0].split(' ').map(Number);

    // Call the logic function
    const result = toggleNthBit(num, n);

    // Print the result
    console.log(result);
});
```