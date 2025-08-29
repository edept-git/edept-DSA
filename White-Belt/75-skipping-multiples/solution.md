# Solutions for Skipping Multiples

### Approach
The problem can be solved by iterating from 1 to `limit` using a `for` loop. Inside the loop, check if the current number is a multiple of `skip_value`. If it is, use the `continue` statement to skip to the next iteration. Otherwise, print the number. The time complexity is O(n) and space complexity is O(1), where n is the limit.

## C Solution
```c
#include <stdio.h>

void skipMultiples(int limit, int skip_value) {
    for (int i = 1; i <= limit; i++) {
        if (i % skip_value == 0) {
            continue;
        }
        printf("%d ", i);
    }
    printf("\n");
}

int main() {
    int limit, skip_value;
    scanf("%d %d", &limit, &skip_value);
    skipMultiples(limit, skip_value);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

void skipMultiples(int limit, int skip_value) {
    for (int i = 1; i <= limit; i++) {
        if (i % skip_value == 0) {
            continue;
        }
        std::cout << i << " ";
    }
    std::cout << std::endl;
}

int main() {
    int limit, skip_value;
    std::cin >> limit >> skip_value;
    skipMultiples(limit, skip_value);
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {
    public static void skipMultiples(int limit, int skip_value) {
        for (int i = 1; i <= limit; i++) {
            if (i % skip_value == 0) {
                continue;
            }
            System.out.print(i + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int limit = scanner.nextInt();
        int skip_value = scanner.nextInt();
        skipMultiples(limit, skip_value);
        scanner.close();
    }
}
```

## Python Solution
```python
def skip_multiples(limit, skip_value):
    result = []
    for i in range(1, limit + 1):
        if i % skip_value == 0:
            continue
        result.append(str(i))
    print(' '.join(result))

if __name__ == "__main__":
    limit, skip_value = map(int, input().split())
    skip_multiples(limit, skip_value)
```

## JavaScript Solution
```javascript
function skipMultiples(limit, skip_value) {
    let result = [];
    for (let i = 1; i <= limit; i++) {
        if (i % skip_value === 0) {
            continue;
        }
        result.push(i);
    }
    console.log(result.join(' '));
}

const readline = require('readline').createInterface({
    input: process.stdin,
    output: process.stdout,
});

readline.question('', line => {
    const [limit, skip_value] = line.split(' ').map(Number);
    skipMultiples(limit, skip_value);
    readline.close();
});
```