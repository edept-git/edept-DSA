# Solutions for Querying Cumulative Sums

### Approach
The most efficient way to handle multiple range sum queries on a static array is by using a technique called **Prefix Sums**. The core idea is to precompute an array where each element stores the sum of all elements up to that point in the original array.

1.  **Prefix Sum Array Construction**: Create a `prefixSum` array of size `N + 1`. Initialize `prefixSum[0]` to `0`. Then, for each index `i` from `0` to `N-1` in the original array `arr`, calculate `prefixSum[i + 1] = prefixSum[i] + arr[i]`. After this step, `prefixSum[k]` will store the sum of elements from `arr[0]` to `arr[k-1]` (inclusive).

2.  **Query Processing**: For each query `(L, R)` (where `L` and `R` are 0-indexed), the sum of elements from `arr[L]` to `arr[R]` can be found by `prefixSum[R + 1] - prefixSum[L]`. This works because `prefixSum[R + 1]` contains the sum `arr[0] + ... + arr[R]`, and `prefixSum[L]` contains `arr[0] + ... + arr[L-1]`. Subtracting the latter from the former leaves exactly `arr[L] + ... + arr[R]`.

**Time Complexity**: Constructing the `prefixSum` array takes `O(N)` time. Each query then takes `O(1)` time. If there are `Q` queries, the total time complexity is `O(N + Q)`. This is significantly better than a naive `O(N*Q)` approach for large `N` and `Q`.

**Space Complexity**: We use an additional `prefixSum` array of size `N + 1`, resulting in `O(N)` space complexity.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int left;
    int right;
} Query;

// Function to solve the range sum queries using prefix sums
// Note: For very large sums, prefixSum should be long long. Given constraints, int is acceptable.
int* solve(int* arr, int n, Query* queries, int numQueries) {
    int* prefixSum = (int*) malloc(sizeof(int) * (n + 1));
    if (prefixSum == NULL) {
        return NULL; // Handle allocation failure
    }
    prefixSum[0] = 0;
    for (int i = 0; i < n; i++) {
        prefixSum[i + 1] = prefixSum[i] + arr[i];
    }

    int* results = (int*) malloc(sizeof(int) * numQueries);
    if (results == NULL) {
        free(prefixSum);
        return NULL; // Handle allocation failure
    }

    for (int i = 0; i < numQueries; i++) {
        int L = queries[i].left;
        int R = queries[i].right;
        // Sum from index L to R (inclusive) is prefixSum[R+1] - prefixSum[L]
        results[i] = prefixSum[R + 1] - prefixSum[L];
    }

    free(prefixSum); // Free allocated prefixSum array
    return results;
}

int main() {
    int n;
    scanf("%d", &n);

    int* arr = (int*) malloc(sizeof(int) * n);
    if (arr == NULL) {
        return 1; // Indicate error
    }
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int numQueries;
    scanf("%d", &numQueries);

    Query* queries = (Query*) malloc(sizeof(Query) * numQueries);
    if (queries == NULL) {
        free(arr);
        return 1; // Indicate error
    }
    for (int i = 0; i < numQueries; i++) {
        scanf("%d %d", &queries[i].left, &queries[i].right);
    }

    int* results = solve(arr, n, queries, numQueries);

    if (results == NULL) {
        free(arr);
        free(queries);
        return 1;
    }

    for (int i = 0; i < numQueries; i++) {
        printf("%d\n", results[i]);
    }

    free(arr);
    free(queries);
    free(results);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric>

struct Query {
    int left;
    int right;
};

// Function to solve the range sum queries using prefix sums
std::vector<int> solve(const std::vector<int>& arr, const std::vector<Query>& queries) {
    int n = arr.size();
    // Use long long for prefixSum to prevent potential overflow, especially if constraints were larger.
    // For current constraints (N=10^5, val=1000), int (max 2*10^9) would technically suffice (max sum 10^8).
    std::vector<long long> prefixSum(n + 1, 0);
    for (int i = 0; i < n; ++i) {
        prefixSum[i + 1] = prefixSum[i] + arr[i];
    }

    std::vector<int> results;
    results.reserve(queries.size()); // Pre-allocate memory for efficiency

    for (const auto& q : queries) {
        int L = q.left;
        int R = q.right;
        // Sum from index L to R (inclusive) is prefixSum[R+1] - prefixSum[L]
        results.push_back(static_cast<int>(prefixSum[R + 1] - prefixSum[L]));
    }
    return results;
}

int main() {
    // Optimize C++ standard streams for competitive programming
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cin >> n;

    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    int numQueries;
    std::cin >> numQueries;

    std::vector<Query> queries(numQueries);
    for (int i = 0; i < numQueries; ++i) {
        std::cin >> queries[i].left >> queries[i].right;
    }

    std::vector<int> results = solve(arr, queries);

    for (int result : results) {
        std::cout << result << "\n";
    }

    return 0;
}
```

## Java Solution
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Query {
    int left;
    int right;

    public Query(int left, int right) {
        this.left = left;
        this.right = right;
    }
}

public class Solution {

    // Function to solve the range sum queries using prefix sums
    public static List<Integer> solve(int[] arr, List<Query> queries) {
        int n = arr.length;
        // Use long for prefixSum to prevent potential overflow, especially if constraints were larger.
        // For current constraints (N=10^5, val=1000), int (max 2*10^9) would technically suffice (max sum 10^8).
        long[] prefixSum = new long[n + 1];
        prefixSum[0] = 0;
        for (int i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + arr[i];
        }

        List<Integer> results = new ArrayList<>();
        for (Query q : queries) {
            int L = q.left;
            int R = q.right;
            // Sum from index L to R (inclusive) is prefixSum[R+1] - prefixSum[L]
            results.add((int)(prefixSum[R + 1] - prefixSum[L]));
        }
        return results;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        int numQueries = scanner.nextInt();
        List<Query> queries = new ArrayList<>();
        for (int i = 0; i < numQueries; i++) {
            int L = scanner.nextInt();
            int R = scanner.nextInt();
            queries.add(new Query(L, R));
        }

        List<Integer> results = solve(arr, queries);

        for (int result : results) {
            System.out.println(result);
        }

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

# Function to solve the range sum queries using prefix sums
def solve(arr, queries):
    n = len(arr)
    prefix_sum = [0] * (n + 1)
    for i in range(n):
        prefix_sum[i + 1] = prefix_sum[i] + arr[i]

    results = []
    for L, R in queries:
        # Sum from index L to R (inclusive) is prefix_sum[R+1] - prefix_sum[L]
        results.append(prefix_sum[R + 1] - prefix_sum[L])
    return results

def main():
    # Read N
    n = int(sys.stdin.readline())

    # Read array elements
    arr = list(map(int, sys.stdin.readline().split()))

    # Read number of queries
    num_queries = int(sys.stdin.readline())

    # Read queries (L, R tuples)
    queries = []
    for _ in range(num_queries):
        L, R = map(int, sys.stdin.readline().split())
        queries.append((L, R)) 

    # Solve and print results
    results = solve(arr, queries)
    for result in results:
        sys.stdout.write(str(result) + "\n")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Function to solve the range sum queries using prefix sums
function solve(arr, queries) {
    const n = arr.length;
    const prefixSum = new Array(n + 1).fill(0);
    for (let i = 0; i < n; i++) {
        prefixSum[i + 1] = prefixSum[i] + arr[i];
    }

    const results = [];
    for (const query of queries) {
        const L = query[0]; // Assuming query is [L, R]
        const R = query[1];
        // Sum from index L to R (inclusive) is prefixSum[R+1] - prefixSum[L]
        results.push(prefixSum[R + 1] - prefixSum[L]);
    }
    return results;
}

function main() {
    const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim().split('\n');
    let lineIndex = 0;

    const n = parseInt(input[lineIndex++]);
    const arr = input[lineIndex++].split(' ').map(Number);

    const numQueries = parseInt(input[lineIndex++]);
    const queries = [];
    for (let i = 0; i < numQueries; i++) {
        queries.push(input[lineIndex++].split(' ').map(Number));
    }

    const results = solve(arr, queries);

    for (const result of results) {
        console.log(result);
    }
}

main();
```