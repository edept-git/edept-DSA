# Solutions for Skipping the Odds, Summing the Evens

### Approach
The solution iterates through the input array using a `for` loop. Inside the loop, an `if` condition checks if the current number is odd. If it is, the `continue` statement skips the rest of the loop body for that iteration and proceeds to the next iteration. If the number is even, it's added to a running sum. Finally, the function returns the calculated sum. The time complexity is O(n) where n is the length of the array, and the space complexity is O(1).

## C Solution
```c
#include <stdio.h>

int sumEvenNumbers(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2 != 0) {
            continue;
        }
        sum += arr[i];
    }
    return sum;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6};
    int size = sizeof(arr) / sizeof(arr[0]);
    int result = sumEvenNumbers(arr, size);
    printf("%d\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sumEvenNumbers(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2 != 0) {
            continue;
        }
        sum += arr[i];
    }
    return sum;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6};
    int size = sizeof(arr) / sizeof(arr[0]);
    int result = sumEvenNumbers(arr, size);
    std::cout << result << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;

public class SumEvens {
    public static int sumEvenNumbers(int[] arr) {
        int sum = 0;
        for (int num : arr) {
            if (num % 2 != 0) {
                continue;
            }
            sum += num;
        }
        return sum;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6};
        int result = sumEvenNumbers(arr);
        System.out.println(result);
    }
}
```

## Python Solution
```python
def sum_even_numbers(arr):
    sum = 0
    for num in arr:
        if num % 2 != 0:
            continue
        sum += num
    return sum

arr = [1, 2, 3, 4, 5, 6]
result = sum_even_numbers(arr)
print(result)
```

## JavaScript Solution
```javascript
function sumEvenNumbers(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] % 2 !== 0) {
            continue;
        }
        sum += arr[i];
    }
    return sum;
}

let arr = [1, 2, 3, 4, 5, 6];
let result = sumEvenNumbers(arr);
console.log(result);
```