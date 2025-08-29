# Solutions for Count Set Bits in a Range

### Approach
The approach involves iterating through numbers from 1 to n. For each number, we count its set bits using a loop and the bitwise AND operator (`&`). We can also optimize by using a lookup table for pre-calculated set bits for faster performance, but for this White Belt problem, a simple iterative approach suffices. The time complexity is O(n*log n) due to the nested loops (iterating through numbers and iterating through bits). The space complexity is O(1) as we use only a few variables.

## C Solution
```c
#include <stdio.h>

int countSetBits(int n) {
    int count = 0;
    for (int i = 1; i <= n; i++) {
        int num = i;
        while (num > 0) {
            count += (num & 1);
            num >>= 1;
        }
    }
    return count;
}

int main() {
    int n;
    scanf("%d", &n);
    printf("%d\n", countSetBits(n));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int countSetBits(int n) {
    int count = 0;
    for (int i = 1; i <= n; i++) {
        int num = i;
        while (num > 0) {
            count += (num & 1);
            num >>= 1;
        }
    }
    return count;
}

int main() {
    int n;
    std::cin >> n;
    std::cout << countSetBits(n) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.*;

public class SetBits {
    public static int countSetBits(int n) {
        int count = 0;
        for (int i = 1; i <= n; i++) {
            int num = i;
            while (num > 0) {
                count += (num & 1);
                num >>= 1;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(countSetBits(n));
        scanner.close();
    }
}
```

## Python Solution
```python
def count_set_bits(n):
    count = 0
    for i in range(1, n + 1):
        num = i
        while num > 0:
            count += (num & 1)
            num >>= 1
    return count

n = int(input())
print(count_set_bits(n))
```

## JavaScript Solution
```javascript
function countSetBits(n) {
    let count = 0;
    for (let i = 1; i <= n; i++) {
        let num = i;
        while (num > 0) {
            count += (num & 1);
            num >>= 1;
        }
    }
    return count;
}

const n = parseInt(process.argv[2]);
console.log(countSetBits(n));
```