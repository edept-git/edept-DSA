# Solutions for Escape the Loop Labyrinth!

### Approach
The solution iterates through the input list.  An 'if' condition checks for the presence of -1, using 'continue' to skip it. Another 'if' checks if the accumulated sum exceeds 100; 'break' exits the loop prematurely. The time complexity is O(n), where n is the length of the list, and space complexity is O(1) as we only use a few variables.

## C Solution
```c
#include <stdio.h>

int sumEvenSkipNegative(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] == -1) {
            continue;
        }
        if (arr[i] % 2 == 0) {
            sum += arr[i];
            if (sum > 100) {
                break;
            }
        }
    }
    return sum;
}

int main() {
    int arr[] = {2, 4, 6, -1, 8, 10, 12, 14, 16, 18, 20};
    int size = sizeof(arr) / sizeof(arr[0]);
    int result = sumEvenSkipNegative(arr, size);
    printf("%d\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sumEvenSkipNegative(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] == -1) {
            continue;
        }
        if (arr[i] % 2 == 0) {
            sum += arr[i];
            if (sum > 100) {
                break;
            }
        }
    }
    return sum;
}

int main() {
    int arr[] = {2, 4, 6, -1, 8, 10, 12, 14, 16, 18, 20};
    int size = sizeof(arr) / sizeof(arr[0]);
    int result = sumEvenSkipNegative(arr, size);
    std::cout << result << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;

public class Main {
    public static int sumEvenSkipNegative(int[] arr) {
        int sum = 0;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == -1) {
                continue;
            }
            if (arr[i] % 2 == 0) {
                sum += arr[i];
                if (sum > 100) {
                    break;
                }
            }
        }
        return sum;
    }

    public static void main(String[] args) {
        int[] arr = {2, 4, 6, -1, 8, 10, 12, 14, 16, 18, 20};
        int result = sumEvenSkipNegative(arr);
        System.out.println(result);
    }
}
```

## Python Solution
```python
def sum_even_skip_negative(arr):
    sum = 0
    for num in arr:
        if num == -1:
            continue
        if num % 2 == 0:
            sum += num
            if sum > 100:
                break
    return sum

arr = [2, 4, 6, -1, 8, 10, 12, 14, 16, 18, 20]
result = sum_even_skip_negative(arr)
print(result)
```

## JavaScript Solution
```javascript
function sumEvenSkipNegative(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === -1) {
            continue;
        }
        if (arr[i] % 2 === 0) {
            sum += arr[i];
            if (sum > 100) {
                break;
            }
        }
    }
    return sum;
}

let arr = [2, 4, 6, -1, 8, 10, 12, 14, 16, 18, 20];
let result = sumEvenSkipNegative(arr);
console.log(result);
```