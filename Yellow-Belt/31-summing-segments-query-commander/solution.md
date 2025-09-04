# Solutions for Summing Segments: Query Commander

### Approach
The most straightforward approach for each query `(L, R)` would be to iterate from `L` to `R` and sum all elements. This would take `O(R - L + 1)` time for each query. In the worst case, if `R - L + 1` is close to `N` and there are `Q` queries, the total time complexity would be `O(Q * N)`, which is too slow for the given constraints (`10^5 * 10^5 = 10^10` operations). 

A more efficient approach involves using **Prefix Sums**. We can pre-compute an array, let's call it `prefix_sum`, where `prefix_sum[i]` stores the sum of all elements from the beginning of the original array up to index `i-1` (inclusive). To handle the sum up to index -1 gracefully, `prefix_sum[0]` is typically initialized to `0`. Then, `prefix_sum[i] = prefix_sum[i-1] + arr[i-1]` for `i > 0`.

After computing the `prefix_sum` array, finding the sum of elements from `arr[L]` to `arr[R]` becomes a simple `O(1)` operation: `sum(L, R) = prefix_sum[R + 1] - prefix_sum[L]`. This works because `prefix_sum[R + 1]` holds the sum from `arr[0]` to `arr[R]`, and `prefix_sum[L]` holds the sum from `arr[0]` to `arr[L-1]`. Subtracting the latter from the former leaves exactly the sum of `arr[L]` to `arr[R]`. 

**Algorithm Steps:**
1.  Read the array size `n` and the array elements `arr`.
2.  Create a `prefix_sum` array of size `n + 1` and initialize `prefix_sum[0]` to `0`.
3.  Populate the `prefix_sum` array: for `i` from `1` to `n`, set `prefix_sum[i] = prefix_sum[i-1] + arr[i-1]`.
4.  Read the number of queries `q`.
5.  For each query, read `L` and `R`.
6.  Calculate `range_sum = prefix_sum[R + 1] - prefix_sum[L]`.
7.  Print `range_sum`.

**Time Complexity:**
*   Pre-computation of `prefix_sum` array: `O(N)`
*   Each query: `O(1)`
*   Total time complexity: `O(N + Q)`

**Space Complexity:**
*   `O(N)` for storing the `prefix_sum` array.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to calculate prefix sums and handle queries
void solve() {
    int n;
    scanf("%d", &n);

    long long *arr = (long long *)malloc(n * sizeof(long long));
    long long *prefix_sum = (long long *)malloc((n + 1) * sizeof(long long));

    if (arr == NULL || prefix_sum == NULL) {
        // Handle memory allocation failure
        if (arr) free(arr);
        if (prefix_sum) free(prefix_sum);
        return;
    }

    prefix_sum[0] = 0;
    for (int i = 0; i < n; i++) {
        scanf("%lld", &arr[i]);
        prefix_sum[i + 1] = prefix_sum[i] + arr[i];
    }

    int q;
    scanf("%d", &q);

    for (int k = 0; k < q; k++) {
        int L, R;
        scanf("%d %d", &L, &R);
        long long range_sum = prefix_sum[R + 1] - prefix_sum[L];
        printf("%lld\n", range_sum);
    }

    free(arr);
    free(prefix_sum);
}

int main() {
    solve();
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

// Function to calculate prefix sums and handle queries
void solve() {
    int n;
    std::cin >> n;

    // Using long long for array elements and prefix sums to prevent overflow
    // as elements can be 10^9 and N can be 10^5, sum can be 10^14.
    std::vector<long long> arr(n);
    std::vector<long long> prefix_sum(n + 1, 0); // Initialize with 0s

    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
        prefix_sum[i + 1] = prefix_sum[i] + arr[i];
    }

    int q;
    std::cin >> q;

    for (int k = 0; k < q; ++k) {
        int L, R;
        std::cin >> L >> R;
        long long range_sum = prefix_sum[R + 1] - prefix_sum[L];
        std::cout << range_sum << "\n";
    }
}

int main() {
    // Optimize C++ standard streams for faster input/output.
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    solve();
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to calculate prefix sums and handle queries
    public static void solve() {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        // Using long for array elements and prefix sums to prevent overflow
        // as elements can be 10^9 and N can be 10^5, sum can be 10^14.
        long[] arr = new long[n];
        long[] prefixSum = new long[n + 1];

        prefixSum[0] = 0;
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextLong();
            prefixSum[i + 1] = prefixSum[i] + arr[i];
        }

        int q = scanner.nextInt();

        for (int k = 0; k < q; k++) {
            int L = scanner.nextInt();
            int R = scanner.nextInt();
            long rangeSum = prefixSum[R + 1] - prefixSum[L];
            System.out.println(rangeSum);
        }

        scanner.close();
    }

    public static void main(String[] args) {
        solve();
    }
}
```

## Python Solution
```python
def solve():
    n = int(input())
    arr = list(map(int, input().split()))

    # Python integers handle arbitrary size, so no explicit long long equivalent is needed.
    prefix_sum = [0] * (n + 1)
    for i in range(n):
        prefix_sum[i + 1] = prefix_sum[i] + arr[i]

    q = int(input())

    results = []
    for _ in range(q):
        L, R = map(int, input().split())
        range_sum = prefix_sum[R + 1] - prefix_sum[L]
        results.append(str(range_sum))
    
    # Print all results at once for potentially faster output with many queries.
    print("\n".join(results))

if __name__ == "__main__":
    solve()
```

## JavaScript Solution
```javascript
function solve() {
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

        const n = parseInt(lines[lineIndex++]);
        const arr = lines[lineIndex++].split(' ').map(Number);

        // JavaScript numbers can represent large integers accurately up to 2^53 - 1.
        // 10^14 is within this safe integer limit, so standard Numbers are fine.
        const prefixSum = new Array(n + 1).fill(0);
        for (let i = 0; i < n; i++) {
            prefixSum[i + 1] = prefixSum[i] + arr[i];
        }

        const q = parseInt(lines[lineIndex++]);
        const results = [];

        for (let k = 0; k < q; k++) {
            const [L, R] = lines[lineIndex++].split(' ').map(Number);
            const rangeSum = prefixSum[R + 1] - prefixSum[L];
            results.push(rangeSum);
        }
        console.log(results.join('\n'));
    });
}

solve(); // Call the main solve function
```