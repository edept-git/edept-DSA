# Solutions for Sum Span: Efficient Range Queries

### Approach
A naive approach would be to iterate through the array from `start` to `end` for each query, summing up the elements. If there are `N` elements and `Q` queries, this would take `O(N)` time per query, leading to an overall time complexity of `O(N * Q)`. For larger `N` or `Q`, this can be inefficient.

To optimize this, we can use the **Prefix Sum** technique. The idea is to pre-compute an array, let's call it `prefixSum`, where `prefixSum[i]` stores the sum of all elements from the beginning of the original array up to (but not including) index `i`. More precisely, `prefixSum[i]` will store the sum of `nums[0]` through `nums[i-1]`. A common convention is:
1.  Initialize `prefixSum` array of size `N+1` with `prefixSum[0] = 0`.
2.  Iterate from `i = 1` to `N`: `prefixSum[i] = prefixSum[i-1] + nums[i-1]`. This takes `O(N)` time to build the `prefixSum` array.
3.  Once the `prefixSum` array is built, for any query `[start, end]`, the sum of elements from `nums[start]` to `nums[end]` (inclusive) can be calculated in `O(1)` time using the formula: `sum = prefixSum[end + 1] - prefixSum[start]`.
    *   `prefixSum[end + 1]` contains the sum `nums[0] + ... + nums[end]`.
    *   `prefixSum[start]` contains the sum `nums[0] + ... + nums[start - 1]`.
    *   Subtracting `prefixSum[start]` from `prefixSum[end + 1]` gives us `(nums[0] + ... + nums[end]) - (nums[0] + ... + nums[start - 1])`, which simplifies to `nums[start] + ... + nums[end]`.

The total time complexity for this approach is `O(N)` for pre-computation and `O(Q)` for all queries, resulting in an overall `O(N + Q)` time complexity. The space complexity is `O(N)` to store the `prefixSum` array.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // For malloc

// Function to calculate range sums using prefix sums
void calculateRangeSums(int* nums, int N, int* queries, int Q) {
    // Create prefix sum array
    // prefixSum[i] stores the sum of nums[0]...nums[i-1]
    // prefixSum has size N+1
    long long* prefixSum = (long long*)malloc((N + 1) * sizeof(long long));
    if (prefixSum == NULL) {
        // Handle memory allocation failure
        return;
    }

    prefixSum[0] = 0;
    for (int i = 0; i < N; i++) {
        prefixSum[i + 1] = prefixSum[i] + nums[i];
    }

    // Process queries
    for (int i = 0; i < Q; i++) {
        int start = queries[i * 2];
        int end = queries[i * 2 + 1];
        // Sum for range [start, end] is prefixSum[end + 1] - prefixSum[start]
        long long sum = prefixSum[end + 1] - prefixSum[start];
        printf("%lld\n", sum);
    }

    free(prefixSum); // Free allocated memory
}

int main() {
    int N;
    scanf("%d", &N);

    int* nums = (int*)malloc(N * sizeof(int));
    if (nums == NULL) {
        // Handle memory allocation failure
        return 1;
    }
    for (int i = 0; i < N; i++) {
        scanf("%d", &nums[i]);
    }

    int Q;
    scanf("%d", &Q);

    // Queries are stored as pairs: [start1, end1, start2, end2, ...]
    int* queries = (int*)malloc(Q * 2 * sizeof(int));
    if (queries == NULL) {
        free(nums);
        return 1;
    }
    for (int i = 0; i < Q * 2; i += 2) {
        scanf("%d %d", &queries[i], &queries[i+1]);
    }

    calculateRangeSums(nums, N, queries, Q);

    free(nums);    // Free allocated memory
    free(queries); // Free allocated memory

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric> 

// Function to calculate range sums using prefix sums
void calculateRangeSums(const std::vector<int>& nums, const std::vector<std::pair<int, int>>& queries) {
    int N = nums.size();
    // Create prefix sum vector
    // prefixSum[i] stores the sum of nums[0]...nums[i-1]
    // prefixSum has size N+1
    std::vector<long long> prefixSum(N + 1, 0);
    for (int i = 0; i < N; ++i) {
        prefixSum[i + 1] = prefixSum[i] + nums[i];
    }

    // Process queries
    for (const auto& query : queries) {
        int start = query.first;
        int end = query.second;
        // Sum for range [start, end] is prefixSum[end + 1] - prefixSum[start]
        long long sum = prefixSum[end + 1] - prefixSum[start];
        std::cout << sum << std::endl;
    }
}

int main() {
    std::ios_base::sync_with_stdio(false); // Optimize C++ standard streams
    std::cin.tie(NULL);

    int N;
    std::cin >> N;

    std::vector<int> nums(N);
    for (int i = 0; i < N; ++i) {
        std::cin >> nums[i];
    }

    int Q;
    std::cin >> Q;

    std::vector<std::pair<int, int>> queries(Q);
    for (int i = 0; i < Q; ++i) {
        std::cin >> queries[i].first >> queries[i].second;
    }

    calculateRangeSums(nums, queries);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;

public class Main {

    // Function to calculate range sums using prefix sums
    public static void calculateRangeSums(int[] nums, List<int[]> queries) {
        int N = nums.length;
        // Create prefix sum array
        // prefixSum[i] stores the sum of nums[0]...nums[i-1]
        // prefixSum has size N+1
        long[] prefixSum = new long[N + 1];
        prefixSum[0] = 0;
        for (int i = 0; i < N; i++) {
            prefixSum[i + 1] = prefixSum[i] + nums[i];
        }

        // Process queries
        for (int[] query : queries) {
            int start = query[0];
            int end = query[1];
            // Sum for range [start, end] is prefixSum[end + 1] - prefixSum[start]
            long sum = prefixSum[end + 1] - prefixSum[start];
            System.out.println(sum);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int N = scanner.nextInt();
        int[] nums = new int[N];
        for (int i = 0; i < N; i++) {
            nums[i] = scanner.nextInt();
        }

        int Q = scanner.nextInt();
        List<int[]> queries = new ArrayList<>();
        for (int i = 0; i < Q; i++) {
            int start = scanner.nextInt();
            int end = scanner.nextInt();
            queries.add(new int[]{start, end});
        }

        calculateRangeSums(nums, queries);

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

# Function to calculate range sums using prefix sums
def calculate_range_sums(nums, queries):
    N = len(nums)
    # Create prefix sum list
    # prefix_sum[i] stores the sum of nums[0]...nums[i-1]
    # prefix_sum has size N+1
    prefix_sum = [0] * (N + 1)
    for i in range(N):
        prefix_sum[i + 1] = prefix_sum[i] + nums[i]

    # Process queries
    results = []
    for start, end in queries:
        # Sum for range [start, end] is prefix_sum[end + 1] - prefix_sum[start]
        current_sum = prefix_sum[end + 1] - prefix_sum[start]
        results.append(str(current_sum))
    
    sys.stdout.write("\n".join(results) + "\n")

if __name__ == "__main__":
    N = int(sys.stdin.readline())
    nums = list(map(int, sys.stdin.readline().split()))

    Q = int(sys.stdin.readline())
    queries = []
    for _ in range(Q):
        start, end = map(int, sys.stdin.readline().split())
        queries.append((start, end))

    calculate_range_sums(nums, queries)
```

## JavaScript Solution
```javascript
// Function to calculate range sums using prefix sums
function calculateRangeSums(nums, queries) {
    const N = nums.length;
    // Create prefix sum array
    // prefixSum[i] stores the sum of nums[0]...nums[i-1]
    // prefixSum has size N+1
    const prefixSum = new Array(N + 1).fill(0);
    for (let i = 0; i < N; i++) {
        prefixSum[i + 1] = prefixSum[i] + nums[i];
    }

    // Process queries
    const results = [];
    for (const query of queries) {
        const start = query[0];
        const end = query[1];
        // Sum for range [start, end] is prefixSum[end + 1] - prefixSum[start]
        const sum = prefixSum[end + 1] - prefixSum[start];
        results.push(sum);
    }
    
    // Output results
    results.forEach(sum => console.log(sum));
}

// Main function to handle input and call the solver
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let lines = [];
    rl.on('line', (line) => {
        lines.push(line);
    }).on('close', () => {
        let lineIndex = 0;

        const N = parseInt(lines[lineIndex++]);
        const nums = lines[lineIndex++].split(' ').map(Number);

        const Q = parseInt(lines[lineIndex++]);
        const queries = [];
        for (let i = 0; i < Q; i++) {
            queries.push(lines[lineIndex++].split(' ').map(Number));
        }

        calculateRangeSums(nums, queries);
    });
}

main();
```