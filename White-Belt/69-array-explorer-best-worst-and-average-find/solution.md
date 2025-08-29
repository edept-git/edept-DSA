# Solutions for Array Explorer: Best, Worst, and Average Find

### Approach
The problem can be solved using a simple linear search. We iterate through the array from the first element to the last, comparing each element with the target. For each comparison made, we increment a counter. If the target is found, we immediately stop and return its index along with the total comparisons made up to that point. If we iterate through the entire array and the target is not found, we return -1 and the total comparisons will be equal to the array's length. This approach uses an array as its primary data structure. The time complexity for the best case (target is the first element) is O(1) because only one comparison is needed. The worst case (target is the last element or not present) is O(N) because we might need to compare with all N elements. The average case also tends towards O(N) as, on average, we would search through about half the array. The space complexity is O(1) as we only use a few constant extra variables for iteration and comparison counting.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h> // For malloc and free

// Structure to hold both the index and comparison count
typedef struct {
    int index;
    int comparisons;
} SearchResult;

// Core logic: Linear search
SearchResult linearSearch(int arr[], int n, int target) {
    SearchResult result;
    result.comparisons = 0;

    for (int i = 0; i < n; i++) {
        result.comparisons++; // Count this comparison
        if (arr[i] == target) {
            result.index = i;
            return result;
        }
    }

    result.index = -1; // Target not found
    return result;
}

int main() {
    int n;
    scanf("%d", &n);

    int *arr = (int *)malloc(n * sizeof(int));
    if (arr == NULL) {
        return 1; // Error
    }

    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int target;
    scanf("%d", &target);

    SearchResult searchResult = linearSearch(arr, n, target);

    if (searchResult.index != -1) {
        printf("Found at index %d in %d comparisons\n", searchResult.index, searchResult.comparisons);
    } else {
        printf("Not found in %d comparisons\n", searchResult.comparisons);
    }

    free(arr); // Clean up allocated memory
    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

// Structure to hold both the index and comparison count
struct SearchResult {
    int index;
    int comparisons;
};

// Core logic: Linear search
SearchResult linearSearch(const std::vector<int>& arr, int target) {
    SearchResult result;
    result.comparisons = 0;

    for (int i = 0; i < arr.size(); ++i) {
        result.comparisons++; // Count this comparison
        if (arr[i] == target) {
            result.index = i;
            return result;
        }
    }

    result.index = -1; // Target not found
    return result;
}

int main() {
    int n;
    std::cin >> n;

    std::vector<int> arr(n);
    for (int i = 0; i < n; ++i) {
        std::cin >> arr[i];
    }

    int target;
    std::cin >> target;

    SearchResult searchResult = linearSearch(arr, target);

    if (searchResult.index != -1) {
        std::cout << "Found at index " << searchResult.index << " in " << searchResult.comparisons << " comparisons" << std::endl;
    } else {
        std::cout << "Not found in " << searchResult.comparisons << " comparisons" << std::endl;
    }

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;

class SearchResult {
    int index;
    int comparisons;

    public SearchResult(int index, int comparisons) {
        this.index = index;
        this.comparisons = comparisons;
    }
}

public class Main {

    // Core logic: Linear search
    public static SearchResult linearSearch(int[] arr, int target) {
        int comparisons = 0;
        for (int i = 0; i < arr.length; i++) {
            comparisons++; // Count this comparison
            if (arr[i] == target) {
                return new SearchResult(i, comparisons);
            }
        }
        return new SearchResult(-1, comparisons); // Target not found
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int n = scanner.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }

        int target = scanner.nextInt();

        SearchResult searchResult = linearSearch(arr, target);

        if (searchResult.index != -1) {
            System.out.println("Found at index " + searchResult.index + " in " + searchResult.comparisons + " comparisons");
        } else {
            System.out.println("Not found in " + searchResult.comparisons + " comparisons");
        }

        scanner.close();
    }
}

```

## Python Solution
```python
def linear_search(arr, target):
    comparisons = 0
    for i in range(len(arr)):
        comparisons += 1  # Count this comparison
        if arr[i] == target:
            return i, comparisons
    return -1, comparisons  # Target not found

def main():
    n = int(input())
    arr = list(map(int, input().split()))
    target = int(input())

    index, comparisons = linear_search(arr, target)

    if index != -1:
        print(f"Found at index {index} in {comparisons} comparisons")
    else:
        print(f"Not found in {comparisons} comparisons")

if __name__ == "__main__":
    main()

```

## JavaScript Solution
```javascript
function linearSearch(arr, target) {
    let comparisons = 0;
    for (let i = 0; i < arr.length; i++) {
        comparisons++; // Count this comparison
        if (arr[i] === target) {
            return { index: i, comparisons: comparisons };
        }
    }
    return { index: -1, comparisons: comparisons }; // Target not found
}

function processInput() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let lines = [];
    rl.on('line', (line) => {
        lines.push(line);
    }).on('close', () => {
        const n = parseInt(lines[0]);
        const arr = lines[1].split(' ').map(Number);
        const target = parseInt(lines[2]);

        const searchResult = linearSearch(arr, target);

        if (searchResult.index !== -1) {
            console.log(`Found at index ${searchResult.index} in ${searchResult.comparisons} comparisons`);
        } else {
            console.log(`Not found in ${searchResult.comparisons} comparisons`);
        }
    });
}

processInput();

```