# Solutions for Array of Wonders: Summing Up the Magic

### Approach
The solution uses a simple iterative approach.  We initialize a variable `sum` to 0. Then, we iterate through the array, adding each element to the `sum` variable.  The time complexity is O(n) where n is the number of elements in the array, as we iterate through the array once. The space complexity is O(1) as we use only a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int calculate_sum(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int sum = calculate_sum(arr, size);
    printf("%d\n", sum);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int calculate_sum(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int sum = calculate_sum(arr, size);
    std::cout << sum << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;

public class ArraySum {

    public static int calculateSum(int[] arr) {
        int sum = 0;
        for (int num : arr) {
            sum += num;
        }
        return sum;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int sum = calculateSum(arr);
        System.out.println(sum);
    }
}
```

## Python Solution
```python
def calculate_sum(arr):
    sum = 0
    for num in arr:
        sum += num
    return sum

arr = [1, 2, 3, 4, 5]
print(calculate_sum(arr))
```

## JavaScript Solution
```javascript
function calculateSum(arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
  }
  return sum;
}

const arr = [1, 2, 3, 4, 5];
console.log(calculateSum(arr));
```