# Solutions for Array Adventures: Sum, Max, and Min

### Approach
The algorithm iterates through the array once.  During this single pass, it calculates the sum, keeps track of the maximum and minimum values encountered so far.  The time complexity is O(n), where n is the number of elements in the array. The space complexity is O(1) because we only use a few extra variables to store the sum, max, and min.

## C Solution
```c
#include <stdio.h>
#include <limits.h>

void array_operations(int arr[], int n, int *sum, int *max, int *min) {
    *sum = 0;
    *max = INT_MIN;
    *min = INT_MAX;
    for (int i = 0; i < n; i++) {
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
    int n;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    int sum, max, min;
    array_operations(arr, n, &sum, &max, &min);
    printf("Sum: %d, Max: %d, Min: %d\n", sum, max, min);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <limits>

void array_operations(int arr[], int n, int &sum, int &max, int &min) {
    sum = 0;
    max = std::numeric_limits<int>::min();
    min = std::numeric_limits<int>::max();
    for (int i = 0; i < n; i++) {
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
    int n;
    std::cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        std::cin >> arr[i];
    }
    int sum, max, min;
    array_operations(arr, n, sum, max, min);
    std::cout << "Sum: " << sum << ", Max: " << max << ", Min: " << min << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
import java.util.Scanner;

public class ArrayOperations {
    public static void arrayOperations(int[] arr) {
        int sum = 0;
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        for (int num : arr) {
            sum += num;
            max = Math.max(max, num);
            min = Math.min(min, num);
        }
        System.out.println("Sum: " + sum + ", Max: " + max + ", Min: " + min);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        arrayOperations(arr);
        scanner.close();
    }
}
```

## Python Solution
```python
def array_operations(arr):
    sum_val = sum(arr)
    max_val = max(arr)
    min_val = min(arr)
    print(f"Sum: {sum_val}, Max: {max_val}, Min: {min_val}")

n = int(input())
arr = list(map(int, input().split()))
array_operations(arr)
```

## JavaScript Solution
```javascript
function arrayOperations(arr) {
  let sum = 0;
  let max = -Infinity;
  let min = Infinity;
  for (let num of arr) {
    sum += num;
    max = Math.max(max, num);
    min = Math.min(min, num);
  }
  console.log(`Sum: ${sum}, Max: ${max}, Min: ${min}`);
}

const n = parseInt(readline());
const arr = readline().split(' ').map(Number);
arrayOperations(arr);
```