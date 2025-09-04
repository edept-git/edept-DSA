# Solutions for Minimal Max Load

### Approach
This problem asks us to minimize the maximum sum assigned to any worker, where tasks must be assigned in contiguous blocks. This is a classic example of "Binary Search on Answer". The answer we are looking for is the minimum possible value for the maximum load among all workers. This value will lie within a certain range.
The search space for our answer (the `max_load`) is defined as follows:
- The lower bound (`low`) for the `max_load` must be at least the largest single task's complexity, because even if `k=n` (each worker gets one task), one worker will have to take the largest task.
- The upper bound (`high`) for the `max_load` is the total sum of all tasks, which occurs if `k=1` (one worker takes all tasks).
We can binary search within this range `[max(tasks), sum(tasks)]`. For each `mid` value in this range, we use a helper "predicate" function, `can_distribute(max_load_limit)`, to determine if it's possible to distribute all tasks among `k` workers such that no worker's total load exceeds `max_load_limit`.

The `can_distribute(max_load_limit)` function works as follows:
Initialize `workers_needed = 1` and `current_worker_load = 0`. Iterate through each task in the `tasks` array.
For each task:
1. Add the task's complexity to `current_worker_load`.
2. If `current_worker_load` exceeds `max_load_limit`:
    - Increment `workers_needed`.
    - Reset `current_worker_load` to the current task's complexity.
Finally, `can_distribute` returns `true` if `workers_needed <= k`, meaning we successfully distributed all tasks using `k` or fewer workers without exceeding `max_load_limit`. Otherwise, it returns `false`.

The main binary search algorithm proceeds:
- Initialize `ans` to `high` (the maximum possible sum).
- While `low <= high`:
    - Calculate `mid = low + (high - low) / 2`.
    - Call `can_distribute(mid)`.
    - If `can_distribute(mid)` returns `true`: It means `mid` is a possible maximum load, and we might be able to do even better (find a smaller `max_load`). So, we update `ans = mid` and try searching in the left half: `high = mid - 1`.
    - If `can_distribute(mid)` returns `false`: It means `mid` is too small; we need a larger `max_load` to distribute all tasks within `k` workers. So, we search in the right half: `low = mid + 1`.
The final `ans` will be the minimum possible maximum load.

Time Complexity: The binary search performs `O(log(Sum))` iterations, where `Sum` is the total sum of all tasks. In each iteration, the `can_distribute` function takes `O(N)` time to iterate through the `tasks` array. Therefore, the total time complexity is `O(N * log(Sum))`.
Space Complexity: `O(1)` (excluding the input array storage).

## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // For malloc, free

// Function to check if it's possible to distribute tasks such that no worker's load exceeds max_load_limit
int canDistribute(const int* tasks, int n, int k, long long max_load_limit) {
    long long current_worker_load = 0;
    int workers_needed = 1;

    for (int i = 0; i < n; ++i) {
        // If adding the current task exceeds the limit, assign it to a new worker
        if (current_worker_load + tasks[i] > max_load_limit) {
            workers_needed++;
            current_worker_load = tasks[i];
        } else {
            current_worker_load += tasks[i];
        }
    }
    return workers_needed <= k;
}

// Main logic function
long long minimalMaxLoad(const int* tasks, int n, int k) {
    if (n == 0) {
        return 0;
    }

    long long low = 0;
    long long high = 0;
    
    // Calculate initial low (max individual task) and high (total sum of tasks)
    for (int i = 0; i < n; ++i) {
        if (tasks[i] > low) { // find max task
            low = tasks[i];
        }
        high += tasks[i]; // sum of all tasks
    }

    long long ans = high; // Initialize answer with the maximum possible load (sum of all tasks)

    // Binary search for the minimal possible maximum load
    while (low <= high) {
        long long mid = low + (high - low) / 2; // Prevent overflow for large low, high
        if (canDistribute(tasks, n, k, mid)) {
            ans = mid; // mid is a possible answer, try for a smaller one in the left half
            high = mid - 1;
        } else {
            low = mid + 1; // mid is too small, need a larger limit, search in the right half
        }
    }
    return ans;
}

int main() {
    int n;
    scanf("%d", &n); // Read number of tasks

    int* tasks = (int*)malloc(n * sizeof(int));
    if (tasks == NULL) {
        return 1; // Error handling for memory allocation
    }

    for (int i = 0; i < n; ++i) {
        scanf("%d", &tasks[i]); // Read task complexities
    }

    int k;
    scanf("%d", &k); // Read number of workers

    long long result = minimalMaxLoad(tasks, n, k);
    printf("%lld\n", result);

    free(tasks); // Free allocated memory
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric>
#include <algorithm>

// Function to check if it's possible to distribute tasks such that no worker's load exceeds max_load_limit
bool canDistribute(const std::vector<int>& tasks, int k, long long max_load_limit) {
    long long current_worker_load = 0;
    int workers_needed = 1;

    for (int task : tasks) {
        // If adding the current task exceeds the limit, assign it to a new worker
        if (current_worker_load + task > max_load_limit) {
            workers_needed++;
            current_worker_load = task;
        } else {
            current_worker_load += task;
        }
    }
    return workers_needed <= k;
}

// Main logic function
long long minimalMaxLoad(const std::vector<int>& tasks, int k) {
    if (tasks.empty()) {
        return 0;
    }

    long long low = 0;
    long long high = 0;
    
    // Calculate initial low (max individual task) and high (total sum of tasks)
    for (int task : tasks) {
        low = std::max(low, (long long)task); // Max individual task
        high += task; // Sum of all tasks
    }

    long long ans = high; // Initialize answer with the maximum possible load (sum of all tasks)

    // Binary search for the minimal possible maximum load
    while (low <= high) {
        long long mid = low + (high - low) / 2; // Prevent overflow for large low, high
        if (canDistribute(tasks, k, mid)) {
            ans = mid; // mid is a possible answer, try for a smaller one in the left half
            high = mid - 1;
        } else {
            low = mid + 1; // mid is too small, need a larger limit, search in the right half
        }
    }
    return ans;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cin >> n; // Read number of tasks

    std::vector<int> tasks(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> tasks[i]; // Read task complexities
    }

    int k;
    std::cin >> k; // Read number of workers

    long long result = minimalMaxLoad(tasks, k);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.Arrays;

public class Main {

    // Function to check if it's possible to distribute tasks such that no worker's load exceeds max_load_limit
    public static boolean canDistribute(int[] tasks, int k, long max_load_limit) {
        long current_worker_load = 0;
        int workers_needed = 1;

        for (int task : tasks) {
            // If adding the current task exceeds the limit, assign it to a new worker
            if (current_worker_load + task > max_load_limit) {
                workers_needed++;
                current_worker_load = task;
            } else {
                current_worker_load += task;
            }
        }
        return workers_needed <= k;
    }

    // Main logic function
    public static long minimalMaxLoad(int[] tasks, int k) {
        if (tasks.length == 0) {
            return 0;
        }

        long low = 0;
        long high = 0;
        
        // Calculate initial low (max individual task) and high (total sum of tasks)
        for (int task : tasks) {
            low = Math.max(low, (long)task); // Max individual task
            high += task; // Sum of all tasks
        }

        long ans = high; // Initialize answer with the maximum possible load (sum of all tasks)

        // Binary search for the minimal possible maximum load
        while (low <= high) {
            long mid = low + (high - low) / 2; // Prevent overflow for large low, high
            if (canDistribute(tasks, k, mid)) {
                ans = mid; // mid is a possible answer, try for a smaller one in the left half
                high = mid - 1;
            } else {
                low = mid + 1; // mid is too small, need a larger limit, search in the right half
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt(); // Read number of tasks
        int[] tasks = new int[n];
        for (int i = 0; i < n; ++i) {
            tasks[i] = scanner.nextInt(); // Read task complexities
        }

        int k = scanner.nextInt(); // Read number of workers

        long result = minimalMaxLoad(tasks, k);
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

def can_distribute(tasks, k, max_load_limit):
    current_worker_load = 0
    workers_needed = 1

    for task in tasks:
        # If adding the current task exceeds the limit, assign it to a new worker
        if current_worker_load + task > max_load_limit:
            workers_needed += 1
            current_worker_load = task
        else:
            current_worker_load += task
    return workers_needed <= k

def minimal_max_load(tasks, k):
    if not tasks:
        return 0

    low = 0
    high = 0
    
    # Calculate initial low (max individual task) and high (total sum of tasks)
    for task in tasks:
        low = max(low, task) # Max individual task
        high += task # Sum of all tasks

    ans = high # Initialize answer with the maximum possible load (sum of all tasks)

    # Binary search for the minimal possible maximum load
    while low <= high:
        mid = low + (high - low) // 2 # Prevent overflow for large low, high
        if can_distribute(tasks, k, mid):
            ans = mid # mid is a possible answer, try for a smaller one in the left half
            high = mid - 1
        else:
            low = mid + 1 # mid is too small, need a larger limit, search in the right half
    return ans

if __name__ == "__main__":
    n = int(sys.stdin.readline()) # Read number of tasks
    tasks = list(map(int, sys.stdin.readline().split())) # Read task complexities

    k = int(sys.stdin.readline()) # Read number of workers

    result = minimal_max_load(tasks, k)
    sys.stdout.write(str(result) + "\n")

```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to check if it's possible to distribute tasks such that no worker's load exceeds max_load_limit
function canDistribute(tasks, k, maxLoadLimit) {
    let currentWorkerLoad = 0;
    let workersNeeded = 1;

    for (let i = 0; i < tasks.length; i++) {
        const task = tasks[i];
        // If adding the current task exceeds the limit, assign it to a new worker
        if (currentWorkerLoad + task > maxLoadLimit) {
            workersNeeded++;
            currentWorkerLoad = task;
        } else {
            currentWorkerLoad += task;
        }
    }
    return workersNeeded <= k;
}

// Main logic function
function minimalMaxLoad(tasks, k) {
    if (tasks.length === 0) {
        return 0;
    }

    let low = 0;
    let high = 0;
    
    // Calculate initial low (max individual task) and high (total sum of tasks)
    for (let i = 0; i < tasks.length; i++) {
        low = Math.max(low, tasks[i]); // Max individual task
        high += tasks[i]; // Sum of all tasks
    }

    let ans = high; // Initialize answer with the maximum possible load (sum of all tasks)

    // Binary search for the minimal possible maximum load
    while (low <= high) {
        let mid = Math.floor(low + (high - low) / 2); // Prevent overflow for large low, high
        if (canDistribute(tasks, k, mid)) {
            ans = mid; // mid is a possible answer, try for a smaller one in the left half
            high = mid - 1;
        } else {
            low = mid + 1; // mid is too small, need a larger limit, search in the right half
        }
    }
    return ans;
}

let inputLines = [];
rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    const n = parseInt(inputLines[0]);
    const tasks = inputLines[1].split(' ').map(Number);
    const k = parseInt(inputLines[2]);

    const result = minimalMaxLoad(tasks, k);
    console.log(result);
});

```