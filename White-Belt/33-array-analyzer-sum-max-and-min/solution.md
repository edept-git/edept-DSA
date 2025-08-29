# Solutions for Array Analyzer: Sum, Max, and Min

### Approach
The solution iterates through the array once to calculate the sum, maximum, and minimum values simultaneously.  This approach has a time complexity of O(n) and a space complexity of O(1), where n is the length of the input array. No extra data structures beyond a few variables are needed.

## C Solution
```c
#include <stdio.h>
#include <limits.h>

void analyze_array(int arr[], int size, int *sum, int *max, int *min) {
    *sum = 0;
    *max = INT_MIN;
    *min = INT_MAX;
    for (int i = 0; i < size; i++) {
        *sum += arr[i];
        if (arr[i] > *max) {
            *max = arr[i];
        }
        if (arr[i] < *min) {
            *min = arr[i];
        }
    }
}

int main() {
    int arr[] = {1, 5, 2, 8, 3};
    int size = sizeof(arr) / sizeof(arr[0]);
    int sum, max, min;
    analyze_array(arr, size, &sum, &max, &min);
    printf("Sum: %d, Max: %d, Min: %d\n", sum, max, min);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <limits>

void analyze_array(int arr[], int size, int &sum, int &max, int &min) {
    sum = 0;
    max = std::numeric_limits<int>::min();
    min = std::numeric_limits<int>::max();
    for (int i = 0; i < size; i++) {
        sum += arr[i];
        if (arr[i] > max) {
            max = arr[i];
        }
        if (arr[i] < min) {
            min = arr[i];
        }
    }
}

int main() {
    int arr[] = {1, 5, 2, 8, 3};
    int size = sizeof(arr) / sizeof(arr[0]);
    int sum, max, min;
    analyze_array(arr, size, sum, max, min);
    std::cout << "Sum: " << sum << ", Max: " << max << ", Min: " << min << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
public class ArrayAnalyzer {
    public static void analyzeArray(int[] arr) {
        int sum = 0;
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        for (int num : arr) {
            sum += num;
            if (num > max) {
                max = num;
            }
            if (num < min) {
                min = num;
            }
        }
        System.out.println("Sum: " + sum + ", Max: " + max + ", Min: " + min);
    }
    public static void main(String[] args) {
        int[] arr = {1, 5, 2, 8, 3};
        analyzeArray(arr);
    }
}
```

## Python Solution
```python
def analyze_array(arr):
    sum_val = sum(arr)
    max_val = max(arr)
    min_val = min(arr)
    print(f"Sum: {sum_val}, Max: {max_val}, Min: {min_val}")

arr = [1, 5, 2, 8, 3]
analyze_array(arr)
```

## JavaScript Solution
```javascript
function analyzeArray(arr) {
  let sum = 0;
  let max = Number.MIN_SAFE_INTEGER;
  let min = Number.MAX_SAFE_INTEGER;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
    if (arr[i] > max) {
      max = arr[i];
    }
    if (arr[i] < min) {
      min = arr[i];
    }
  }
  console.log(`Sum: ${sum}, Max: ${max}, Min: ${min}`);
}

let arr = [1, 5, 2, 8, 3];
analyzeArray(arr);
```