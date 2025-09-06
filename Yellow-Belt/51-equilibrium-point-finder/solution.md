# Solutions for Equilibrium Point Finder

### Approach
The most efficient way to solve this problem is by using a single pass after an initial sum calculation. First, calculate the `total_sum` of all elements in the array. Then, initialize a `left_sum` variable to `0`. Iterate through the array from the first element to the last. In each iteration at index `i` with element `arr[i]`, calculate the `right_sum` by subtracting `arr[i]` and the current `left_sum` from the `total_sum` (`right_sum = total_sum - left_sum - arr[i]`). If `left_sum` is equal to `right_sum`, then `i` is an equilibrium point, and since we are looking for the *first* one, we can return `i` immediately. After checking, update `left_sum` by adding `arr[i]` to it for the next iteration. If the loop completes without finding any such index, return -1.

This approach uses `O(N)` time complexity for iterating through the array twice (once for total sum, once for finding equilibrium) and `O(1)` space complexity as it only requires a few auxiliary variables.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to find the first equilibrium point
int findEquilibriumPoint(int arr[], int n) {
    if (n == 0) {
        return -1;
    }

    long long totalSum = 0;
    for (int i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    long long leftSum = 0;
    for (int i = 0; i < n; i++) {
        // rightSum = totalSum - leftSum - arr[i]
        // Note: For a single element array, leftSum is 0, rightSum is 0. So index 0 is an equilibrium point.
        if (leftSum == (totalSum - leftSum - arr[i])) {
            return i;
        }
        leftSum += arr[i];
    }

    return -1;
}

int main() {
    int n;
    scanf("%d", &n);

    int *arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        return 1; // Memory allocation failed
    }

    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int result = findEquilibriumPoint(arr, n);
    printf("%d\n", result);

    free(arr);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric>

// Function to find the first equilibrium point
int findEquilibriumPoint(const std::vector<int>& arr) {
    int n = arr.size();
    if (n == 0) {
        return -1;
    }

    long long totalSum = 0;
    for (int x : arr) {
        totalSum += x;
    }

    long long leftSum = 0;
    for (int i = 0; i < n; ++i) {
        // rightSum = totalSum - leftSum - arr[i]
        // Note: For a single element array, leftSum is 0, rightSum is 0. So index 0 is an equilibrium point.
        if (leftSum == (totalSum - leftSum - arr[i])) {
            return i;
        }
        leftSum += arr[i];
    }

    return -1;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cin >> n;

    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    int result = findEquilibriumPoint(arr);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to find the first equilibrium point
    public static int findEquilibriumPoint(int[] arr) {
        int n = arr.length;
        if (n == 0) {
            return -1;
        }

        long totalSum = 0;
        for (int x : arr) {
            totalSum += x;
        }

        long leftSum = 0;
        for (int i = 0; i < n; i++) {
            // rightSum = totalSum - leftSum - arr[i]
            // Note: For a single element array, leftSum is 0, rightSum is 0. So index 0 is an equilibrium point.
            if (leftSum == (totalSum - leftSum - arr[i])) {
                return i;
            }
            leftSum += arr[i];
        }

        return -1;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        scanner.close();

        int result = findEquilibriumPoint(arr);
        System.out.println(result);
    }
}
```

## Python Solution
```python
import sys

def find_equilibrium_point(arr):
    n = len(arr)
    if n == 0:
        return -1

    total_sum = sum(arr)
    left_sum = 0

    for i in range(n):
        # right_sum = total_sum - left_sum - arr[i]
        # Note: For a single element array, left_sum is 0, right_sum is 0. So index 0 is an equilibrium point.
        if left_sum == (total_sum - left_sum - arr[i]):
            return i
        left_sum += arr[i]

    return -1

def main():
    n = int(sys.stdin.readline())
    arr = list(map(int, sys.stdin.readline().split()))

    result = find_equilibrium_point(arr)
    sys.stdout.write(str(result) + '\n')

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to find the first equilibrium point
function findEquilibriumPoint(arr) {
    const n = arr.length;
    if (n === 0) {
        return -1;
    }

    let totalSum = 0;
    for (let i = 0; i < n; i++) {
        totalSum += arr[i];
    }

    let leftSum = 0;
    for (let i = 0; i < n; i++) {
        // rightSum = totalSum - leftSum - arr[i]
        // Note: For a single element array, leftSum is 0, rightSum is 0. So index 0 is an equilibrium point.
        if (leftSum === (totalSum - leftSum - arr[i])) {
            return i;
        }
        leftSum += arr[i];
    }

    return -1;
}

let input = [];
rl.on('line', (line) => {
    input.push(line);
}).on('close', () => {
    const n = parseInt(input[0]);
    const arr = input[1].split(' ').map(Number);

    const result = findEquilibriumPoint(arr);
    console.log(result);
});
```