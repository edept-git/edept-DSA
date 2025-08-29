# Solutions for The Case of the Curious Comparisons

### Approach
The problem requires analyzing the number of comparisons needed to find the minimum element in an unsorted array.  A simple linear scan is used. 

* **Best Case:** The minimum element is at the beginning of the array. Only 0 comparisons are needed because the first element is already the minimum.

* **Worst Case:** The minimum element is at the end of the array.  The algorithm needs to compare every element (n-1 comparisons) before finding the minimum.

* **Average Case:** Assuming the minimum element is roughly in the middle of the array, the average number of comparisons will be approximately n/2.  Since the array is unsorted, this is an approximation. 

The time complexity is O(n) for all three cases because we iterate through the entire array in the worst case. The space complexity is O(1) as we only use a constant amount of extra space.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

int minComparisons(int arr[], int n) {
    int min_val = arr[0];
    int comparisons = 0;
    for (int i = 1; i < n; i++) {
        comparisons++;
        if (arr[i] < min_val) {
            min_val = arr[i];
        }
    }
    return comparisons;
}

int main() {
    int arr[] = {3, 1, 4, 1, 5, 9, 2, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    printf("Best Case: 0, Worst Case: %d, Average Case: %d\n", n - 1, n / 2);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

using namespace std;

int minComparisons(vector<int>& arr) {
    int min_val = arr[0];
    int comparisons = 0;
    for (int i = 1; i < arr.size(); i++) {
        comparisons++;
        if (arr[i] < min_val) {
            min_val = arr[i];
        }
    }
    return comparisons;
}

int main() {
    vector<int> arr = {3, 1, 4, 1, 5, 9, 2, 6};
    int n = arr.size();
    cout << "Best Case: 0, Worst Case: " << n - 1 << ", Average Case: " << n / 2 << endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
public class MinComparisons {
    public static int minComparisons(int[] arr) {
        int min_val = arr[0];
        int comparisons = 0;
        for (int i = 1; i < arr.length; i++) {
            comparisons++;
            if (arr[i] < min_val) {
                min_val = arr[i];
            }
        }
        return comparisons;
    }
    public static void main(String[] args) {
        int[] arr = {3, 1, 4, 1, 5, 9, 2, 6};
        int n = arr.length;
        System.out.println("Best Case: 0, Worst Case: " + (n - 1) + ", Average Case: " + n / 2);
    }
}
```

## Python Solution
```python
def min_comparisons(arr):
    min_val = arr[0]
    comparisons = 0
    for i in range(1, len(arr)):
        comparisons += 1
        if arr[i] < min_val:
            min_val = arr[i]
    return comparisons

arr = [3, 1, 4, 1, 5, 9, 2, 6]

n = len(arr)
print(f"Best Case: 0, Worst Case: {n - 1}, Average Case: {n // 2}")
```

## JavaScript Solution
```javascript
function minComparisons(arr) {
    let min_val = arr[0];
    let comparisons = 0;
    for (let i = 1; i < arr.length; i++) {
        comparisons++;
        if (arr[i] < min_val) {
            min_val = arr[i];
        }
    }
    return comparisons;
}

let arr = [3, 1, 4, 1, 5, 9, 2, 6];
let n = arr.length;
console.log("Best Case: 0, Worst Case: " + (n - 1) + ", Average Case: " + Math.floor(n / 2));
```