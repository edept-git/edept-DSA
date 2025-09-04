# Solutions for Subarray Summit: Maximize Your Gains

### Approach
This problem can be efficiently solved using Kadane's Algorithm, which is a classic dynamic programming approach. The core idea is to maintain two variables during a single pass through the array: `current_max` and `global_max`. `current_max` stores the maximum sum of a subarray ending at the current position. For each element `nums[i]`, `current_max` is updated to be the maximum of `nums[i]` (starting a new subarray from this element) or `current_max + nums[i]` (extending the existing subarray). This way, if `current_max` becomes negative, it's reset to `nums[i]`, effectively discarding the preceding negative sum. `global_max` keeps track of the overall maximum sum found anywhere in the array so far, updated at each step with `max(global_max, current_max)`. We initialize `global_max` and `current_max` with the first element of the array to correctly handle cases where all numbers are negative. The algorithm iterates through the array once, leading to a time complexity of O(N), where N is the number of elements in the array. Since we only use a few constant extra variables, the space complexity is O(1).

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function implementing Kadane's Algorithm
int maxSubArraySum(int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0; // Or handle as an error, based on specific requirements
    }

    int max_so_far = nums[0];
    int current_max = nums[0];

    for (int i = 1; i < numsSize; i++) {
        current_max = max(nums[i], current_max + nums[i]);
        max_so_far = max(max_so_far, current_max);
    }

    return max_so_far;
}

int main() {
    int n;
    // Read the number of elements
    if (scanf("%d", &n) != 1) {
        return 1;
    }

    if (n <= 0) {
        printf("0\n"); // Constraints say 1 <= n
        return 0;
    }

    int* nums = (int*)malloc(n * sizeof(int));
    if (nums == NULL) {
        return 1; // Malloc failed
    }

    // Read the array elements
    for (int i = 0; i < n; i++) {
        if (scanf("%d", &nums[i]) != 1) {
            free(nums);
            return 1;
        }
    }

    // Calculate and print the result
    int result = maxSubArraySum(nums, n);
    printf("%d\n", result);

    free(nums);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // Required for std::max
#include <limits>    // Required for std::numeric_limits

// Function implementing Kadane's Algorithm
int maxSubArraySum(const std::vector<int>& nums) {
    if (nums.empty()) {
        return 0; // Or throw an exception, based on specific requirements
    }

    int max_so_far = nums[0];
    int current_max = nums[0];

    for (size_t i = 1; i < nums.size(); ++i) {
        current_max = std::max(nums[i], current_max + nums[i]);
        max_so_far = std::max(max_so_far, current_max);
    }

    return max_so_far;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    // Read the number of elements
    std::cin >> n;

    if (n <= 0) {
        std::cout << 0 << std::endl; // Constraints say 1 <= n
        return 0;
    }

    std::vector<int> nums(n);
    // Read the array elements
    for (int i = 0; i < n; ++i) {
        std::cin >> nums[i];
    }

    // Calculate and print the result
    int result = maxSubArraySum(nums);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function implementing Kadane's Algorithm
    public static int maxSubArraySum(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0; // Or throw an exception, based on specific requirements
        }

        int maxSoFar = nums[0];
        int currentMax = nums[0];

        for (int i = 1; i < nums.length; i++) {
            currentMax = Math.max(nums[i], currentMax + nums[i]);
            maxSoFar = Math.max(maxSoFar, currentMax);
        }

        return maxSoFar;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the number of elements
        int n = scanner.nextInt();

        if (n <= 0) {
            System.out.println(0); // Constraints say 1 <= n
            scanner.close();
            return;
        }

        int[] nums = new int[n];
        // Read the array elements
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }

        // Calculate and print the result
        int result = maxSubArraySum(nums);
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

def max_subarray_sum(nums: list[int]) -> int:
    if not nums:
        return 0 # Constraints say 1 <= n

    max_so_far = nums[0]
    current_max = nums[0]

    for i in range(1, len(nums)):
        current_max = max(nums[i], current_max + nums[i])
        max_so_far = max(max_so_far, current_max)

    return max_so_far

if __name__ == '__main__':
    # Read the number of elements
    n = int(sys.stdin.readline())

    if n <= 0:
        print(0) # Constraints say 1 <= n
    else:
        # Read the array elements
        # Assuming elements are space-separated on a single line
        nums_str = sys.stdin.readline().strip().split()
        nums = [int(x) for x in nums_str]

        # Calculate and print the result
        result = max_subarray_sum(nums)
        print(result)

```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function implementing Kadane's Algorithm
function maxSubarraySum(nums) {
    if (!nums || nums.length === 0) {
        return 0; // Or handle as an error, based on specific requirements
    }

    let maxSoFar = nums[0];
    let currentMax = nums[0];

    for (let i = 1; i < nums.length; i++) {
        currentMax = Math.max(nums[i], currentMax + nums[i]);
        maxSoFar = Math.max(maxSoFar, currentMax);
    }

    return maxSoFar;
}

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    const n = parseInt(inputLines[0], 10);

    if (n <= 0) {
        console.log(0); // Constraints say 1 <= n
        return;
    }

    // Assuming elements are space-separated on the second line
    const nums = inputLines[1].split(' ').map(Number);

    // Calculate and print the result
    const result = maxSubarraySum(nums);
    console.log(result);
});
```