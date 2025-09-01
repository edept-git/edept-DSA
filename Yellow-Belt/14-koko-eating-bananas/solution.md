# Solutions for Koko Eating Bananas

### Approach
The core idea is to use binary search on the possible values of Koko's eating speed `k`. The minimum possible `k` is 1 (Koko eats at least one banana per hour). The maximum possible `k` is the size of the largest pile (`max(piles)`), because if Koko eats at this speed, she can finish any pile in at most one hour, which is the fastest possible way. So, our search space for `k` is `[1, max(piles)]`.

Inside the binary search, for a given `mid` value (which represents a potential `k`), we calculate the total time Koko would take to eat all bananas. For each pile `p` in `piles`, the time taken is `(p + mid - 1) / mid` (using integer ceiling division). We sum these times up. If the `total_time` is less than or equal to `h`, it means `mid` is a possible answer, and we might even be able to find a smaller `k`. So, we update our `ans = mid` and try searching in the lower half `[low, mid - 1]`. If `total_time` is greater than `h`, it means `mid` is too slow, and we need a faster `k`. We then search in the upper half `[mid + 1, high]`.

The binary search continues until `low` crosses `high`, and the final `ans` will be the minimum `k` that satisfies the condition.

**Time Complexity**: `O(N log M)`, where `N` is the number of piles (`piles.length`) and `M` is the maximum number of bananas in a pile (`max(piles)`). The `log M` factor comes from the binary search iterations, and in each iteration, we loop through all `N` piles to calculate the total time.
**Space Complexity**: `O(1)`, as we only use a few extra variables for the binary search and calculations.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Helper function to calculate total hours for a given eating speed k
long long calculate_hours(int* piles, int pilesSize, int k) {
    long long total_h = 0;
    for (int i = 0; i < pilesSize; i++) {
        // Equivalent to ceil(piles[i] / k)
        total_h += (piles[i] + k - 1) / k;
    }
    return total_h;
}

int minEatingSpeed(int* piles, int pilesSize, int h) {
    int low = 1;
    int high = 0; // Max pile size
    for (int i = 0; i < pilesSize; i++) {
        if (piles[i] > high) {
            high = piles[i];
        }
    }

    int ans = high;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (calculate_hours(piles, pilesSize, mid) <= h) {
            ans = mid;
            high = mid - 1; // Try to find a smaller k
        } else {
            low = mid + 1; // Need a faster k
        }
    }
    return ans;
}

int main() {
    int pilesSize;
    scanf("%d", &pilesSize);

    int* piles = (int*)malloc(pilesSize * sizeof(int));
    for (int i = 0; i < pilesSize; i++) {
        scanf("%d", &piles[i]);
    }

    int h;
    scanf("%d", &h);

    int result = minEatingSpeed(piles, pilesSize, h);
    printf("%d\n", result);

    free(piles);
    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>
#include <cmath>

// Helper function to calculate total hours for a given eating speed k
long long calculateHours(const std::vector<int>& piles, int k) {
    long long totalHours = 0;
    for (int p : piles) {
        // Equivalent to ceil((double)p / k)
        totalHours += (p + k - 1) / k;
    }
    return totalHours;
}

int minEatingSpeed(std::vector<int>& piles, int h) {
    int low = 1;
    // The maximum possible speed is the largest pile size
    // (Koko eats the largest pile in one hour, and then the rest within h)
    int high = *std::max_element(piles.begin(), piles.end());

    int ans = high;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (calculateHours(piles, mid) <= h) {
            ans = mid;
            high = mid - 1; // Try to find a smaller k
        } else {
            low = mid + 1; // Need a faster k
        }
    }
    return ans;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int pilesSize;
    std::cin >> pilesSize;

    std::vector<int> piles(pilesSize);
    for (int i = 0; i < pilesSize; ++i) {
        std::cin >> piles[i];
    }

    int h;
    std::cin >> h;

    int result = minEatingSpeed(piles, h);
    std::cout << result << std::endl;

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;
import java.util.Arrays;

public class Solution {

    // Helper function to calculate total hours for a given eating speed k
    private static long calculateHours(int[] piles, int k) {
        long totalHours = 0;
        for (int p : piles) {
            // Equivalent to Math.ceil((double) p / k)
            totalHours += (p + k - 1) / k;
        }
        return totalHours;
    }

    public static int minEatingSpeed(int[] piles, int h) {
        int low = 1;
        int high = 0; // Max pile size
        for (int p : piles) {
            if (p > high) {
                high = p;
            }
        }

        int ans = high;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (calculateHours(piles, mid) <= h) {
                ans = mid;
                high = mid - 1; // Try to find a smaller k
            } else {
                low = mid + 1; // Need a faster k
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int pilesSize = scanner.nextInt();
        int[] piles = new int[pilesSize];
        for (int i = 0; i < pilesSize; i++) {
            piles[i] = scanner.nextInt();
        }

        int h = scanner.nextInt();

        int result = minEatingSpeed(piles, h);
        System.out.println(result);

        scanner.close();
    }
}

```

## Python Solution
```python
import math

def calculate_hours(piles, k):
    total_hours = 0
    for p in piles:
        # Equivalent to math.ceil(p / k)
        total_hours += (p + k - 1) // k
    return total_hours

def minEatingSpeed(piles, h):
    low = 1
    high = max(piles) # The maximum possible speed is the largest pile size

    ans = high

    while low <= high:
        mid = low + (high - low) // 2
        if calculate_hours(piles, mid) <= h:
            ans = mid
            high = mid - 1 # Try to find a smaller k
        else:
            low = mid + 1 # Need a faster k
    return ans

if __name__ == '__main__':
    piles_size = int(input())
    piles = list(map(int, input().split()))
    h = int(input())

    result = minEatingSpeed(piles, h)
    print(result)

```

## JavaScript Solution
```javascript
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
    const pilesSize = parseInt(inputLines[0]);
    const piles = inputLines[1].split(' ').map(Number);
    const h = parseInt(inputLines[2]);

    const result = minEatingSpeed(piles, h);
    console.log(result);
});

// Helper function to calculate total hours for a given eating speed k
function calculateHours(piles, k) {
    let totalHours = 0;
    for (const p of piles) {
        // Equivalent to Math.ceil(p / k)
        totalHours += Math.ceil(p / k);
    }
    return totalHours;
}

function minEatingSpeed(piles, h) {
    let low = 1;
    let high = Math.max(...piles); // The maximum possible speed is the largest pile size

    let ans = high;

    while (low <= high) {
        let mid = Math.floor(low + (high - low) / 2);
        if (calculateHours(piles, mid) <= h) {
            ans = mid;
            high = mid - 1; // Try to find a smaller k
        } else {
            low = mid + 1; // Need a faster k
        }
    }
    return ans;
}

```