# Solutions for Array Sum, Max, and Min Trio

### Approach
The solution iterates through the array once to calculate the sum, maximum, and minimum values simultaneously.  It initializes the sum to 0, the maximum to the first element, and the minimum to the first element.  Then, for each element in the array, the sum is updated by adding the current element. The maximum and minimum values are updated if the current element is greater than the current maximum or smaller than the current minimum, respectively. This approach has a time complexity of O(n) and a space complexity of O(1), where n is the length of the array.

## C Solution
```c
#include <stdio.h>
#include <limits.h>

void arrayStats(int arr[], int n, int *sum, int *max, int *min) {
    *sum = 0;
    *max = INT_MIN;
    *min = INT_MAX;
    for (int i = 0; i < n; i++) {
        *sum += arr[i];
        if (arr[i] > *max) *max = arr[i];
        if (arr[i] < *min) *min = arr[i];
    }
}

int main() {
    int arr[] = {1, 5, 2, 8, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum, max, min;
    arrayStats(arr, n, &sum, &max, &min);
    printf("Sum: %d, Max: %d, Min: %d\n", sum, max, min);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <limits>

void arrayStats(int arr[], int n, int &sum, int &max, int &min) {
    sum = 0;
    max = std::numeric_limits<int>::min();
    min = std::numeric_limits<int>::max();
    for (int i = 0; i < n; i++) {
        sum += arr[i];
        if (arr[i] > max) max = arr[i];
        if (arr[i] < min) min = arr[i];
    }
}

int main() {
    int arr[] = {1, 5, 2, 8, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum, max, min;
    arrayStats(arr, n, sum, max, min);
    std::cout << "Sum: " << sum << ", Max: " << max << ", Min: " << min << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;

public class ArrayStats {
    public static void arrayStats(int[] arr, int[] result) {
        result[0] = 0;
        result[1] = Integer.MIN_VALUE;
        result[2] = Integer.MAX_VALUE;
        for (int num : arr) {
            result[0] += num;
            if (num > result[1]) result[1] = num;
            if (num < result[2]) result[2] = num;
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 5, 2, 8, 3};
        int[] result = new int[3];
        arrayStats(arr, result);
        System.out.println("Sum: " + result[0] + ", Max: " + result[1] + ", Min: " + result[2]);
    }
}
```

## Python Solution
```python
def array_stats(arr):
    sum_val = 0
    max_val = float('-inf')
    min_val = float('inf')
    for num in arr:
        sum_val += num
        max_val = max(max_val, num)
        min_val = min(min_val, num)
    return sum_val, max_val, min_val

arr = [1, 5, 2, 8, 3]
sum, max, min = array_stats(arr)
print(f"Sum: {sum}, Max: {max}, Min: {min}")
```

## JavaScript Solution
```javascript
function arrayStats(arr) {
  let sum = 0;
  let max = Number.MIN_SAFE_INTEGER;
  let min = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
    if (arr[i] > max) max = arr[i];
    if (arr[i] < min) min = arr[i];
  }
  return { sum, max, min };
}

let arr = [1, 5, 2, 8, 3];
let stats = arrayStats(arr);
console.log(`Sum: ${stats.sum}, Max: ${stats.max}, Min: ${stats.min}`);
```