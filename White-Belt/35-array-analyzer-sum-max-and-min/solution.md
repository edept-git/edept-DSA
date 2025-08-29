# Solutions for Array Analyzer: Sum, Max, and Min

### Approach
The algorithm iterates through the input array once.  It initializes the sum to 0, the maximum to the first element, and the minimum to the first element. During each iteration, it adds the current element to the sum, updates the maximum if the current element is greater, and updates the minimum if the current element is smaller. The time complexity is O(n), where n is the length of the array, and the space complexity is O(1) because it uses a constant amount of extra space.

## C Solution
```c
#include <stdio.h>
#include <limits.h>

void analyze_array(int arr[], int n, int *sum, int *max, int *min) {
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
    int n, sum, max, min;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    analyze_array(arr, n, &sum, &max, &min);
    printf("Sum: %d, Max: %d, Min: %d\n", sum, max, min);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <limits>

void analyze_array(int arr[], int n, int &sum, int &max, int &min) {
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
    int n;
    std::cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        std::cin >> arr[i];
    }
    int sum, max, min;
    analyze_array(arr, n, sum, max, min);
    std::cout << "Sum: " << sum << ", Max: " << max << ", Min: " << min << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
import java.util.Scanner;

public class ArrayAnalyzer {

    public static void analyzeArray(int[] arr) {
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
        analyzeArray(arr);
        scanner.close();
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

n = int(input())
arr = list(map(int, input().split()))
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
    max = Math.max(max, arr[i]);
    min = Math.min(min, arr[i]);
  }
  console.log(`Sum: ${sum}, Max: ${max}, Min: ${min}`);
}

const n = parseInt(readline());
const arr = readline().split(' ').map(Number);
analyzeArray(arr);
```