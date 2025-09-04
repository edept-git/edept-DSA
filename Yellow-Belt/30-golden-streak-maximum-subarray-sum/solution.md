# Solutions for Golden Streak: Maximum Subarray Sum

### Approach
This problem can be efficiently solved using Kadane's Algorithm, which is a classic example of dynamic programming and a greedy approach. The core idea is to iterate through the array, maintaining two variables: `current_max` and `max_so_far`. `current_max` tracks the maximum sum of a subarray ending at the current position. For each element `num`, `current_max` is updated to be the maximum of `num` itself (starting a new subarray) or `num + current_max` (extending the existing subarray). This effectively decides whether it's better to include the current number in the running sum or to start a new subarray from the current number. `max_so_far` keeps track of the overall maximum sum encountered throughout the iteration, updating itself with `current_max` if `current_max` is greater. Both `current_max` and `max_so_far` are initialized with the first element of the array. This approach correctly handles cases with all negative numbers by ensuring that the single largest negative number is returned. The time complexity of this algorithm is O(N) because we iterate through the array once. The space complexity is O(1) as we only use a few constant extra variables.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

// Function to find the maximum of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Function to find the maximum subarray sum using Kadane's Algorithm
int maxSubArraySum(int* nums, int numsSize) {
    if (numsSize == 0) {
        return 0; // Or handle error as per problem constraints
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
    int* nums = NULL;
    int capacity = 10; // Initial capacity
    int numsSize = 0;
    int num;

    nums = (int*)malloc(capacity * sizeof(int));
    if (nums == NULL) {
        return 1; // Malloc failed
    }

    // Read space-separated integers from stdin until newline or EOF
    while (scanf("%d", &num) == 1) {
        if (numsSize == capacity) {
            capacity *= 2;
            int* temp = (int*)realloc(nums, capacity * sizeof(int));
            if (temp == NULL) {
                free(nums);
                return 1; // Realloc failed
            }
            nums = temp;
        }
        nums[numsSize++] = num;

        // Check for newline character, assuming input is on a single line
        char next_char = getchar();
        if (next_char == '\n' || next_char == EOF) {
            ungetc(next_char, stdin); // Put it back if it's EOF for potential future reads (though not needed here)
            break;
        }
        ungetc(next_char, stdin); // Put back any non-space/non-digit character to be re-read if it's not a separator
    }

    // Consume the rest of the line to clear buffer if any chars are left (like a final newline not caught by scanf)
    while (getchar() != '\n' && !feof(stdin));

    printf("%d\n", maxSubArraySum(nums, numsSize));

    free(nums);
    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
#include <sstream>

// Function to find the maximum subarray sum using Kadane's Algorithm
int maxSubArraySum(const std::vector<int>& nums) {
    if (nums.empty()) {
        return 0; // Or handle error as per problem constraints
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
    std::string line;
    std::getline(std::cin, line);
    std::stringstream ss(line);
    std::vector<int> nums;
    int num;

    while (ss >> num) {
        nums.push_back(num);
    }

    std::cout << maxSubArraySum(nums) << std::endl;

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;

public class Solution {

    // Function to find the maximum subarray sum using Kadane's Algorithm
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0; // Or handle error as per problem constraints
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
        List<Integer> numList = new ArrayList<>();

        String line = scanner.nextLine();
        String[] strNums = line.trim().split("\\s+"); // Split by one or more spaces

        for (String strNum : strNums) {
            if (!strNum.isEmpty()) {
                numList.add(Integer.parseInt(strNum));
            }
        }

        int[] nums = new int[numList.size()];
        for (int i = 0; i < numList.size(); i++) {
            nums[i] = numList.get(i);
        }

        Solution sol = new Solution();
        System.out.println(sol.maxSubArray(nums));

        scanner.close();
    }
}

```

## Python Solution
```python
import sys

def max_sub_array_sum(nums: list[int]) -> int:
    if not nums:
        return 0 # Or handle error as per problem constraints

    max_so_far = nums[0]
    current_max = nums[0]

    for i in range(1, len(nums)):
        current_max = max(nums[i], current_max + nums[i])
        max_so_far = max(max_so_far, current_max)
    
    return max_so_far

if __name__ == '__main__':
    # Read space-separated integers from stdin
    line = sys.stdin.readline().strip()
    nums = list(map(int, line.split()))
    
    result = max_sub_array_sum(nums)
    print(result)

```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to find the maximum subarray sum using Kadane's Algorithm
function maxSubArraySum(nums) {
    if (nums.length === 0) {
        return 0; // Or handle error as per problem constraints
    }

    let maxSoFar = nums[0];
    let currentMax = nums[0];

    for (let i = 1; i < nums.length; i++) {
        currentMax = Math.max(nums[i], currentMax + nums[i]);
        maxSoFar = Math.max(maxSoFar, currentMax);
    }

    return maxSoFar;
}

rl.on('line', (line) => {
    const nums = line.split(' ').map(Number);
    const result = maxSubArraySum(nums);
    console.log(result);
    rl.close();
});

```