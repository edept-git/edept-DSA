# Solutions for Cyclic Countdown

### Approach
This problem can be solved using basic arithmetic and the modulo operator. To find the day of the week after a certain number of days have passed, we first sum the `startDay` and `daysPassed`. Since the days of the week cycle every 7 days (0-6), we can use the modulo 7 operation on the sum. This will give us the remainder, which corresponds to the new day of the week. The time complexity of this approach is O(1) because it involves a fixed number of arithmetic operations. The space complexity is also O(1) as it only uses a few variables to store the input and the result.

## C Solution
```c
#include <stdio.h>

// Function to calculate the future day of the week
int calculateFutureDay(int startDay, int daysPassed) {
    // Calculate the total number of days from Monday (day 0)
    // Then use modulo 7 to find the equivalent day in the 0-6 range
    return (startDay + daysPassed) % 7;
}

int main() {
    int startDay, daysPassed;

    // Read the starting day from stdin
    scanf("%d", &startDay);

    // Read the number of days passed from stdin
    scanf("%d", &daysPassed);

    // Calculate the future day
    int futureDay = calculateFutureDay(startDay, daysPassed);

    // Print the result to stdout
    printf("%d\n", futureDay);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

// Function to calculate the future day of the week
int calculateFutureDay(int startDay, int daysPassed) {
    // Calculate the total number of days from Monday (day 0)
    // Then use modulo 7 to find the equivalent day in the 0-6 range
    return (startDay + daysPassed) % 7;
}

int main() {
    int startDay, daysPassed;

    // Read the starting day from stdin
    std::cin >> startDay;

    // Read the number of days passed from stdin
    std::cin >> daysPassed;

    // Calculate the future day
    int futureDay = calculateFutureDay(startDay, daysPassed);

    // Print the result to stdout
    std::cout << futureDay << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate the future day of the week
    public static int calculateFutureDay(int startDay, int daysPassed) {
        // Calculate the total number of days from Monday (day 0)
        // Then use modulo 7 to find the equivalent day in the 0-6 range
        return (startDay + daysPassed) % 7;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the starting day from stdin
        int startDay = scanner.nextInt();

        // Read the number of days passed from stdin
        int daysPassed = scanner.nextInt();

        // Calculate the future day
        int futureDay = calculateFutureDay(startDay, daysPassed);

        // Print the result to stdout
        System.out.println(futureDay);

        scanner.close();
    }
}
```

## Python Solution
```python
def calculate_future_day(start_day, days_passed):
    # Calculate the total number of days from Monday (day 0)
    # Then use modulo 7 to find the equivalent day in the 0-6 range
    return (start_day + days_passed) % 7

if __name__ == "__main__":
    # Read the starting day from stdin
    start_day = int(input())

    # Read the number of days passed from stdin
    days_passed = int(input())

    # Calculate the future day
    future_day = calculate_future_day(start_day, days_passed)

    # Print the result to stdout
    print(future_day)
```

## JavaScript Solution
```javascript
function calculateFutureDay(startDay, daysPassed) {
    // Calculate the total number of days from Monday (day 0)
    // Then use modulo 7 to find the equivalent day in the 0-6 range
    return (startDay + daysPassed) % 7;
}

// Read input from stdin
// For typical competitive programming environments in JS, input is often read line by line.
// This example assumes two lines of input, one for startDay and one for daysPassed.
let input = '';
process.stdin.on('data', data => {
    input += data;
});

process.stdin.on('end', () => {
    const lines = input.trim().split('\n');
    const startDay = parseInt(lines[0], 10);
    const daysPassed = parseInt(lines[1], 10);

    const futureDay = calculateFutureDay(startDay, daysPassed);
    console.log(futureDay);
});
```