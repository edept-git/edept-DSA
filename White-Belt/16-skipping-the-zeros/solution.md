# Solutions for Skipping the Zeros

### Approach
The solution iterates through the input array.  A `for` loop is used to traverse the array.  If a zero is encountered, the `continue` statement skips the rest of the current iteration and proceeds to the next. If a negative number is encountered, the `break` statement terminates the loop. Otherwise, the positive number is printed. The time complexity is O(n), where n is the length of the array, and the space complexity is O(1).

## C Solution
```c
#include <stdio.h>

void processArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        if (arr[i] == 0) {
            continue;
        }
        if (arr[i] < 0) {
            break;
        }
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {1, 0, 2, 0, 3, -1, 4, 0, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    processArray(arr, size);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

void processArray(const std::vector<int>& arr) {
    for (int num : arr) {
        if (num == 0) {
            continue;
        }
        if (num < 0) {
            break;
        }
        std::cout << num << " ";
    }
    std::cout << std::endl;
}

int main() {
    std::vector<int> arr = {1, 0, 2, 0, 3, -1, 4, 0, 5};
    processArray(arr);
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;

public class SkipZeros {
    public static void processArray(int[] arr) {
        for (int num : arr) {
            if (num == 0) {
                continue;
            }
            if (num < 0) {
                break;
            }
            System.out.print(num + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int[] arr = {1, 0, 2, 0, 3, -1, 4, 0, 5};
        processArray(arr);
    }
}
```

## Python Solution
```python
def process_array(arr):
    for num in arr:
        if num == 0:
            continue
        if num < 0:
            break
        print(num, end=" ")
    print()

arr = [1, 0, 2, 0, 3, -1, 4, 0, 5]
process_array(arr)
```

## JavaScript Solution
```javascript
function processArray(arr) {
    for (let num of arr) {
        if (num === 0) {
            continue;
        }
        if (num < 0) {
            break;
        }
        process.stdout.write(num + " ");
    }
    console.log();
}

let arr = [1, 0, 2, 0, 3, -1, 4, 0, 5];
processArray(arr);
```