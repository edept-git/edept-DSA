# Solutions for Find the Largest Element: Best, Worst, and Average Case

### Approach
The solution uses a linear search algorithm to find the largest element in the array.  We iterate through the array, keeping track of the largest element found so far. 

**Best Case:** The best case occurs when the largest element is the first element in the array. The time complexity is O(1). 

**Worst Case:** The worst case occurs when the largest element is the last element in the array. The time complexity is O(n), where n is the number of elements in the array. 

**Average Case:**  The average case time complexity is also O(n), as we expect to examine approximately half of the array elements on average before finding the largest element. The space complexity is O(1) as we only use a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int findLargest(int arr[], int n) {
    int largest = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }
    return largest;
}

int main() {
    int n;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    int largest = findLargest(arr, n);
    printf("%d\n", largest);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

int findLargest(const std::vector<int>& arr) {
    int largest = arr[0];
    for (int i = 1; i < arr.size(); ++i) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }
    return largest;
}

int main() {
    int n;
    std::cin >> n;
    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }
    std::cout << findLargest(arr) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
import java.util.Scanner;

public class LargestElement {

    public static int findLargest(int[] arr) {
        int largest = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > largest) {
                largest = arr[i];
            }
        }
        return largest;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        System.out.println(findLargest(arr));
        scanner.close();
    }
}
```

## Python Solution
```python
def findLargest(arr):
    largest = arr[0]
    for i in range(1, len(arr)):
        if arr[i] > largest:
            largest = arr[i]
    return largest

n = int(input())
arr = list(map(int, input().split()))
print(findLargest(arr))
```

## JavaScript Solution
```javascript
function findLargest(arr) {
  let largest = arr[0];
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > largest) {
      largest = arr[i];
    }
  }
  return largest;
}

const n = parseInt(readline());
const arr = readline().split(' ').map(Number);
print(findLargest(arr));
```