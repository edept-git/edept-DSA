# Solutions for Find the Maximum Element (Best, Worst, Average Case)

### Approach
The problem is solved using a linear search.  We iterate through the array, keeping track of the maximum element found so far. 

**Best Case:** The maximum element is the first element of the array. Time Complexity: O(1)

**Worst Case:** The maximum element is the last element of the array. Time Complexity: O(n)

**Average Case:** The maximum element is somewhere in the middle of the array. Time Complexity: O(n)

Space Complexity: O(1) as we are using a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int findMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

int main() {
    int n;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    int max = findMax(arr, n);
    printf("%d\n", max);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

int findMax(const std::vector<int>& arr) {
    int max = arr[0];
    for (int i = 1; i < arr.size(); ++i) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

int main() {
    int n;
    std::cin >> n;
    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }
    int max = findMax(arr);
    std::cout << max << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
import java.util.Scanner;

public class MaxElement {
    public static int findMax(int[] arr) {
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        return max;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        int max = findMax(arr);
        System.out.println(max);
        scanner.close();
    }
}
```

## Python Solution
```python
def findMax(arr):
    max = arr[0]
    for i in range(1, len(arr)):
        if arr[i] > max:
            max = arr[i]
    return max

n = int(input())
arr = list(map(int, input().split()))
max = findMax(arr)
print(max)
```

## JavaScript Solution
```javascript
function findMax(arr) {
  let max = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }
  return max;
}

const n = parseInt(readline());
const arr = readline().split(' ').map(Number);
const max = findMax(arr);
print(max);
```