# Solutions for Binary Quest: Find Your Target

### Approach
The core of this problem lies in implementing binary search, an efficient algorithm for finding an item from a sorted list of items. There are two common ways to implement it: iteratively or recursively. For this solution, we will detail the iterative approach, which often avoids potential stack overflow issues that recursive solutions might face with very large input arrays.

The iterative binary search works by maintaining two pointers, `low` and `high`, initially pointing to the start (index 0) and end (index `n-1`) of the array, respectively. In each step, we calculate the middle index `mid = low + (high - low) / 2`. This calculation for `mid` is preferred over `(low + high) / 2` to prevent potential integer overflow if `low` and `high` are very large. We then compare the element at `nums[mid]` with the `target`:

1.  If `nums[mid]` equals `target`, we have found the element and return `mid`.
2.  If `nums[mid]` is less than `target`, it means the target, if present, must be in the right half of the array. We update `low = mid + 1` to continue searching in the right subarray.
3.  If `nums[mid]` is greater than `target`, it means the target, if present, must be in the left half of the array. We update `high = mid - 1` to continue searching in the left subarray.

This process continues as long as `low <= high`. If the loop finishes without finding the target, it means the target is not present in the array, and we return -1.

The time complexity of binary search is O(log n) because the search space is halved in each step. The space complexity for the iterative approach is O(1), as it only uses a few variables regardless of the input size.

## C Solution
```c
#include <stdio.h>

// Function to perform iterative binary search
int binarySearch(int* nums, int n, int target) {
    int low = 0;
    int high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // Prevent potential overflow

        if (nums[mid] == target) {
            return mid; // Target found at mid index
        } else if (nums[mid] < target) {
            low = mid + 1; // Target is in the right half
        } else { // nums[mid] > target
            high = mid - 1; // Target is in the left half
        }
    }
    return -1; // Target not found
}

int main() {
    int n;
    scanf("%d", &n);

    int nums[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &nums[i]);
    }

    int target;
    scanf("%d", &target);

    int result = binarySearch(nums, n, target);
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

// Function to perform iterative binary search
int binarySearch(const std::vector<int>& nums, int target) {
    int low = 0;
    int high = nums.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // Prevent potential overflow

        if (nums[mid] == target) {
            return mid; // Target found at mid index
        } else if (nums[mid] < target) {
            low = mid + 1; // Target is in the right half
        } else { // nums[mid] > target
            high = mid - 1; // Target is in the left half
        }
    }
    return -1; // Target not found
}

int main() {
    int n;
    std::cin >> n;

    std::vector<int> nums(n);
    for (int i = 0; i < n; i++) {
        std::cin >> nums[i];
    }

    int target;
    std::cin >> target;

    int result = binarySearch(nums, target);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to perform iterative binary search
    public static int binarySearch(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2; // Prevent potential overflow

            if (nums[mid] == target) {
                return mid; // Target found at mid index
            } else if (nums[mid] < target) {
                low = mid + 1; // Target is in the right half
            } else { // nums[mid] > target
                high = mid - 1; // Target is in the left half
            }
        }
        return -1; // Target not found
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }

        int target = scanner.nextInt();

        int result = binarySearch(nums, target);
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
def binary_search(nums, target):
    low = 0
    high = len(nums) - 1

    while low <= high:
        mid = low + (high - low) // 2  # Prevent potential overflow

        if nums[mid] == target:
            return mid  # Target found at mid index
        elif nums[mid] < target:
            low = mid + 1  # Target is in the right half
        else:  # nums[mid] > target
            high = mid - 1  # Target is in the left half
    return -1  # Target not found

if __name__ == '__main__':
    n = int(input())
    nums = list(map(int, input().split()))
    target = int(input())

    result = binary_search(nums, target)
    print(result)
```

## JavaScript Solution
```javascript
function binarySearch(nums, target) {
    let low = 0;
    let high = nums.length - 1;

    while (low <= high) {
        let mid = Math.floor(low + (high - low) / 2); // Prevent potential overflow

        if (nums[mid] === target) {
            return mid; // Target found at mid index
        } else if (nums[mid] < target) {
            low = mid + 1; // Target is in the right half
        } else { // nums[mid] > target
            high = mid - 1; // Target is in the left half
        }
    }
    return -1; // Target not found
}

function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let input = [];
    rl.on('line', (line) => {
        input.push(line);
    }).on('close', () => {
        const n = parseInt(input[0]);
        const nums = input[1].split(' ').map(Number);
        const target = parseInt(input[2]);

        const result = binarySearch(nums, target);
        console.log(result);
    });
}

main();
```