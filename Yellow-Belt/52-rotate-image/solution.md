# Solutions for Rotate Image

### Approach
The most efficient way to rotate a square matrix 90 degrees clockwise in-place involves two main steps:

First, we **transpose the matrix**. Transposing means changing rows into columns and columns into rows. For every element at `matrix[i][j]`, we swap it with `matrix[j][i]`. We only need to do this for elements where `j > i` to avoid swapping elements twice or swapping an element with itself.

Second, after transposing, the matrix is oriented in a way that allows a 90-degree clockwise rotation to be completed by **reversing each row** of the now-transposed matrix. For each row, we swap the first element with the last, the second with the second-to-last, and so on, until the entire row is reversed.

By combining these two steps (transpose then reverse each row), we achieve the desired 90-degree clockwise rotation in-place.

**Time Complexity**: O(N^2), where N is the dimension of the square matrix. This is because we iterate through roughly half the elements for transposing and then iterate through all elements for reversing rows, leading to a constant number of operations per element.
**Space Complexity**: O(1), as we perform all operations directly on the input matrix without using any extra significant storage.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to rotate the matrix
void rotate(int** matrix, int n) {
    // 1. Transpose the matrix
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }

    // 2. Reverse each row
    for (int i = 0; i < n; i++) {
        int left = 0;
        int right = n - 1;
        while (left < right) {
            int temp = matrix[i][left];
            matrix[i][left] = matrix[i][right];
            matrix[i][right] = temp;
            left++;
            right--;
        }
    }
}

int main() {
    int n;
    // Input format: first line is N, then N lines of N space-separated integers
    // Example:
    // 3
    // 1 2 3
    // 4 5 6
    // 7 8 9
    scanf("%d", &n);

    // Allocate memory for the matrix
    int** matrix = (int**)malloc(n * sizeof(int*));
    for (int i = 0; i < n; i++) {
        matrix[i] = (int*)malloc(n * sizeof(int));
        for (int j = 0; j < n; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }

    // Rotate the matrix
    rotate(matrix, n);

    // Print the rotated matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d%s", matrix[i][j], (j == n - 1) ? "" : " ");
        }
        printf("\n");
    }

    // Free allocated memory
    for (int i = 0; i < n; i++) {
        free(matrix[i]);
    }
    free(matrix);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::swap and std::reverse

// Function to rotate the matrix
void rotate(std::vector<std::vector<int>>& matrix) {
    int n = matrix.size();

    // 1. Transpose the matrix
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            std::swap(matrix[i][j], matrix[j][i]);
        }
    }

    // 2. Reverse each row
    for (int i = 0; i < n; i++) {
        std::reverse(matrix[i].begin(), matrix[i].end());
    }
}

int main() {
    int n;
    // Input format: first line is N, then N lines of N space-separated integers
    // Example:
    // 3
    // 1 2 3
    // 4 5 6
    // 7 8 9
    std::cin >> n;

    std::vector<std::vector<int>> matrix(n, std::vector<int>(n));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            std::cin >> matrix[i][j];
        }
    }

    // Rotate the matrix
    rotate(matrix);

    // Print the rotated matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            std::cout << matrix[i][j] << (j == n - 1 ? "" : " ");
        }
        std::cout << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // 1. Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // 2. Reverse each row
        for (int i = 0; i < n; i++) {
            int left = 0;
            int right = n - 1;
            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Input format: first line is N, then N lines of N space-separated integers
        // Example:
        // 3
        // 1 2 3
        // 4 5 6
        // 7 8 9
        int n = scanner.nextInt();

        int[][] matrix = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        Solution sol = new Solution();
        sol.rotate(matrix);

        // Print the rotated matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(matrix[i][j] + (j == n - 1 ? "" : " "));
            }
            System.out.println();
        }

        scanner.close();
    }
}
```

## Python Solution
```python
class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        # 1. Transpose the matrix
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # 2. Reverse each row
        for i in range(n):
            matrix[i].reverse() # Python's list.reverse() is convenient

def main():
    # Input format: first line is N, then N lines of N space-separated integers
    # Example:
    # 3
    # 1 2 3
    # 4 5 6
    # 7 8 9
    n = int(input())
    matrix = []
    for _ in range(n):
        matrix.append(list(map(int, input().split())))

    sol = Solution()
    sol.rotate(matrix)

    # Print the rotated matrix
    for row in matrix:
        print(*(row)) # Python's print(*row) will print elements separated by space

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
function rotate(matrix) {
    const n = matrix.length;

    // 1. Transpose the matrix
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]]; // ES6 destructuring for swap
        }
    }

    // 2. Reverse each row
    for (let i = 0; i < n; i++) {
        matrix[i].reverse(); // Array.prototype.reverse() is convenient
    }
}

// Function to handle input and output for testing
function main() {
    // Input format: first line is N, then N lines of N space-separated integers
    // Example:
    // 3
    // 1 2 3
    // 4 5 6
    // 7 8 9
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let n = 0;
    let matrix = [];
    let lineNum = 0;

    rl.on('line', (line) => {
        if (lineNum === 0) {
            n = parseInt(line);
        } else {
            matrix.push(line.split(' ').map(Number));
        }
        lineNum++;

        if (lineNum > n) { // All lines of matrix data read
            rotate(matrix);

            // Print the rotated matrix
            for (let i = 0; i < n; i++) {
                console.log(matrix[i].join(' '));
            }
            rl.close();
        }
    });
}

if (require.main === module) {
    main();
}
```