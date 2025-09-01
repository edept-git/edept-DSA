# Solutions for Kth Missing Positive Number

### Approach
The problem can be efficiently solved using binary search. The key idea is to recognize that for any element `arr[i]` at index `i`, the number of positive integers missing *before or at* `arr[i]` is `arr[i] - (i + 1)`. This is because if all numbers from `1` to `arr[i]` were present, there would be `arr[i]` numbers, but we only have `i + 1` numbers (`arr[0]` to `arr[i]`). The difference tells us how many are missing. This function `f(i) = arr[i] - (i + 1)` is monotonically increasing with `i`.

We can use binary search to find the smallest index `idx` such that `arr[idx] - (idx + 1)` (the count of missing numbers up to `arr[idx]`) is greater than or equal to `k`.
1.  Initialize `low = 0` and `high = arr.length - 1`.
2.  While `low <= high`:
    a.  Calculate `mid = low + (high - low) / 2`.
    b.  Calculate the number of missing positives before `arr[mid]`: `missing_count = arr[mid] - (mid + 1)`.
    c.  If `missing_count < k`: This means the `k`-th missing number is further to the right (or beyond the array). We need to consider elements with more missing numbers, so set `low = mid + 1`.
    d.  Else (`missing_count >= k`): This means we have found at least `k` missing numbers up to `arr[mid]`. The `k`-th missing number might be `arr[mid]` itself (though unlikely) or something before it. We try to find a smaller `arr[mid]` or an earlier position, so set `high = mid - 1`.
3.  After the loop, the `low` pointer will indicate the first index where `arr[low] - (low + 1)` would be `>= k`. The `k`-th missing positive number will be `low + k`.

**Time Complexity**: O(log N), where N is the length of the array `arr`, due to the binary search.
**Space Complexity**: O(1), as we only use a few extra variables.


## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

int findKthPositive(int* arr, int arrSize, int k) {
    int low = 0;
    int high = arrSize - 1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        // Count of missing numbers before arr[mid]
        // If all numbers from 1 to arr[mid] were present, there would be arr[mid] numbers.
        // But we only have (mid + 1) numbers (arr[0] to arr[mid]).
        // So, arr[mid] - (mid + 1) gives the count of missing numbers.
        if (arr[mid] - (mid + 1) < k) {
            low = mid + 1; // Not enough missing numbers, look in the right half
        } else {
            high = mid - 1; // Enough missing numbers, try to find an earlier position
        }
    }
    
    // After the loop, 'low' will be the index where the k-th missing number would be.
    // The k-th missing number is simply 'low + k'.
    return low + k;
}

int main() {
    int arr_size, k;

    // Read arr_size
    scanf("%d", &arr_size);

    // Allocate memory for the array
    int* arr = (int*)malloc(arr_size * sizeof(int));

    // Read array elements
    for (int i = 0; i < arr_size; i++) {
        scanf("%d", &arr[i]);
    }

    // Read k
    scanf("%d", &k);

    // Call the function and print the result
    int result = findKthPositive(arr, arr_size, k);
    printf("%d\n", result);

    // Free allocated memory
    free(arr);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric>

class Solution {
public:
    int findKthPositive(std::vector<int>& arr, int k) {
        int low = 0;
        int high = arr.size() - 1;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            // Count of missing numbers before arr[mid]
            // If all numbers from 1 to arr[mid] were present, there would be arr[mid] numbers.
            // But we only have (mid + 1) numbers (arr[0] to arr[mid]).
            // So, arr[mid] - (mid + 1) gives the count of missing numbers.
            if (arr[mid] - (mid + 1) < k) {
                low = mid + 1; // Not enough missing numbers, look in the right half
            } else {
                high = mid - 1; // Enough missing numbers, try to find an earlier position
            }
        }
        
        // After the loop, 'low' will be the index where the k-th missing number would be.
        // The k-th missing number is simply 'low + k'.
        return low + k;
    }
};

int main() {
    int n, k;
    std::cin >> n; // Read array size

    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i]; // Read array elements
    }

    std::cin >> k; // Read k

    Solution sol;
    int result = sol.findKthPositive(arr, k);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {
    public int findKthPositive(int[] arr, int k) {
        int low = 0;
        int high = arr.length - 1;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            // Count of missing numbers before arr[mid]
            // If all numbers from 1 to arr[mid] were present, there would be arr[mid] numbers.
            // But we only have (mid + 1) numbers (arr[0] to arr[mid]).
            // So, arr[mid] - (mid + 1) gives the count of missing numbers.
            if (arr[mid] - (mid + 1) < k) {
                low = mid + 1; // Not enough missing numbers, look in the right half
            } else {
                high = mid - 1; // Enough missing numbers, try to find an earlier position
            }
        }
        
        // After the loop, 'low' will be the index where the k-th missing number would be.
        // The k-th missing number is simply 'low + k'.
        return low + k;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read array size
        int n = scanner.nextInt();
        int[] arr = new int[n];

        // Read array elements
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        // Read k
        int k = scanner.nextInt();

        Solution sol = new Solution();
        int result = sol.findKthPositive(arr, k);
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
class Solution:
    def findKthPositive(self, arr: list[int], k: int) -> int:
        low = 0
        high = len(arr) - 1
        
        while low <= high:
            mid = low + (high - low) // 2
            # Count of missing numbers before arr[mid]
            # If all numbers from 1 to arr[mid] were present, there would be arr[mid] numbers.
            # But we only have (mid + 1) numbers (arr[0] to arr[mid]).
            # So, arr[mid] - (mid + 1) gives the count of missing numbers.
            if arr[mid] - (mid + 1) < k:
                low = mid + 1  # Not enough missing numbers, look in the right half
            else:
                high = mid - 1 # Enough missing numbers, try to find an earlier position
            
        # After the loop, 'low' will be the index where the k-th missing number would be.
        # The k-th missing number is simply 'low + k'.
        return low + k

def main():
    # Read array size
    n = int(input())
    # Read array elements
    arr = list(map(int, input().split()))
    # Read k
    k = int(input())

    sol = Solution()
    result = sol.findKthPositive(arr, k)
    print(result)

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number}
 */
var findKthPositive = function(arr, k) {
    let low = 0;
    let high = arr.length - 1;
    
    while (low <= high) {
        let mid = Math.floor(low + (high - low) / 2);
        // Count of missing numbers before arr[mid]
        // If all numbers from 1 to arr[mid] were present, there would be arr[mid] numbers.
        // But we only have (mid + 1) numbers (arr[0] to arr[mid]).
        // So, arr[mid] - (mid + 1) gives the count of missing numbers.
        if (arr[mid] - (mid + 1) < k) {
            low = mid + 1; // Not enough missing numbers, look in the right half
        } else {
            high = mid - 1; // Enough missing numbers, try to find an earlier position
        }
    }
    
    // After the loop, 'low' will be the index where the k-th missing number would be.
    // The k-th missing number is simply 'low + k'.
    return low + k;
};

// Main function for handling input/output
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let inputLines = [];
    rl.on('line', (line) => {
        inputLines.push(line);
    }).on('close', () => {
        let n = parseInt(inputLines[0]);
        let arr = inputLines[1].split(' ').map(Number);
        let k = parseInt(inputLines[2]);

        let result = findKthPositive(arr, k);
        console.log(result);
    });
}

// Call main to start the program
if (require.main === module) {
    main();
}
```