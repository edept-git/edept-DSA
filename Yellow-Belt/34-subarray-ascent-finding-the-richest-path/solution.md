# Solutions for Subarray Ascent: Finding the Richest Path

### Approach
This problem can be efficiently solved using Kadane's Algorithm, which is a classic dynamic programming approach optimized to a greedy solution. The algorithm iterates through the array, keeping track of two main variables: `current_max` and `global_max`. `current_max` represents the maximum sum of a subarray ending at the current position. As we traverse the array, for each element, we decide whether to extend the current subarray by adding the element to `current_max` or to start a new subarray from the current element if adding it would make the `current_max` smaller than the element itself (i.e., `current_max + num < num`). More simply, `current_max = max(num, current_max + num)`. The `global_max` keeps track of the maximum sum found across all subarrays encountered so far. It is updated at each step: `global_max = max(global_max, current_max)`. Both `current_max` and `global_max` are initialized with the first element of the array. This approach ensures that we always maintain the maximum sum ending at the current position, and from those, we pick the overall maximum. This leads to a time complexity of O(N) because we iterate through the array once, and a space complexity of O(1) as we only use a few constant extra variables.

## C Solution
```c
#include <stdio.h>
#include <limits.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to find the maximum subarray sum using Kadane's algorithm
int maxSubArray(int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0; // Or handle as an error, depending on constraints. Constraints say numsSize >= 1.
    }

    int current_max = nums[0];
    int global_max = nums[0];

    for (int i = 1; i < numsSize; i++) {
        current_max = max(nums[i], current_max + nums[i]);
        global_max = max(global_max, current_max);
    }

    return global_max;
}

int main() {
    int numsSize;
    scanf("%d", &numsSize);

    int nums[numsSize]; // VLA for dynamic array, C99 standard
    for (int i = 0; i < numsSize; i++) {
        scanf("%d", &nums[i]);
    }

    int result = maxSubArray(nums, numsSize);
    printf("%d\n", result);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::max

// Function to find the maximum subarray sum using Kadane's algorithm
int maxSubArray(const std::vector<int>& nums) {
    if (nums.empty()) {
        return 0; // Constraints state nums.length >= 1, but good practice.
    }

    int current_max = nums[0];
    int global_max = nums[0];

    for (size_t i = 1; i < nums.size(); ++i) {
        current_max = std::max(nums[i], current_max + nums[i]);
        global_max = std::max(global_max, current_max);
    }

    return global_max;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cin >> n;

    std::vector<int> nums(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> nums[i];
    }

    int result = maxSubArray(nums);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to find the maximum subarray sum using Kadane's algorithm
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0; // Constraints state nums.length >= 1, but good practice.
        }

        int currentMax = nums[0];
        int globalMax = nums[0];

        for (int i = 1; i < nums.length; i++) {
            currentMax = Math.max(nums[i], currentMax + nums[i]);
            globalMax = Math.max(globalMax, currentMax);
        }

        return globalMax;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = scanner.nextInt();
        }
        scanner.close();

        Solution sol = new Solution();
        int result = sol.maxSubArray(nums);
        System.out.println(result);
    }
}
```

## Python Solution
```python
import sys

def max_sub_array(nums: list[int]) -> int:
    if not nums:
        return 0  # Constraints state nums.length >= 1, but good practice.

    current_max = nums[0]
    global_max = nums[0]

    for i in range(1, len(nums)):
        current_max = max(nums[i], current_max + nums[i])
        global_max = max(global_max, current_max)

    return global_max

if __name__ == '__main__':
    n = int(sys.stdin.readline())
    nums = list(map(int, sys.stdin.readline().split()))

    result = max_sub_array(nums)
    sys.stdout.write(str(result) + "\n")
```

## JavaScript Solution
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
function maxSubArray(nums) {
    if (nums.length === 0) {
        return 0; // Constraints state nums.length >= 1, but good practice.
    }

    let currentMax = nums[0];
    let globalMax = nums[0];

    for (let i = 1; i < nums.length; i++) {
        currentMax = Math.max(nums[i], currentMax + nums[i]);
        globalMax = Math.max(globalMax, currentMax);
    }

    return globalMax;
}

// Handle input and output for competitive programming environment
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    const n = parseInt(inputLines[0]);
    const nums = inputLines[1].split(' ').map(Number);
    
    const result = maxSubArray(nums);
    console.log(result);
});
```