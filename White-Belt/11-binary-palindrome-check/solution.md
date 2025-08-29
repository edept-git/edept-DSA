# Solutions for Binary Palindrome Check

### Approach
The algorithm involves converting the integer to its binary representation, then reversing the binary string and comparing it to the original.  We can achieve the reversal using bitwise operations or string manipulation.  Time complexity is O(log n) due to the binary conversion, where n is the input integer. Space complexity is O(log n) to store the binary string.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int isBinaryPalindrome(int n) {
    if (n < 0) return 0;
    char binary[33]; 
    int i = 0;
    while (n > 0) {
        binary[i++] = (n % 2) + '0';
        n /= 2;
    }
    binary[i] = '\0';
    int len = strlen(binary);
    for (int j = 0; j < len / 2; j++) {
        if (binary[j] != binary[len - 1 - j]) return 0;
    }
    return 1;
}

int main() {
    int n;
    scanf("%d", &n);
    printf("%s\n", isBinaryPalindrome(n) ? "true" : "false");
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <algorithm>

using namespace std;

bool isBinaryPalindrome(int n) {
    if (n < 0) return false;
    string binary = "";
    while (n > 0) {
        binary = (n % 2 == 0 ? "0" : "1") + binary;
        n /= 2;
    }
    string reversed_binary = binary;
    reverse(reversed_binary.begin(), reversed_binary.end());
    return binary == reversed_binary;
}

int main() {
    int n;
    cin >> n;
    cout << (isBinaryPalindrome(n) ? "true" : "false") << endl;
    return 0;
}
```

## Java Solution
```java
import java.util.*;

public class BinaryPalindrome {
    public static boolean isBinaryPalindrome(int n) {
        if (n < 0) return false;
        String binary = Integer.toBinaryString(n);
        String reversedBinary = new StringBuilder(binary).reverse().toString();
        return binary.equals(reversedBinary);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        System.out.println(isBinaryPalindrome(n));
        scanner.close();
    }
}
```

## Python Solution
```python
def is_binary_palindrome(n):
    if n < 0:
        return False
    binary = bin(n)[2:]
    return binary == binary[::-1]

n = int(input())
print("true" if is_binary_palindrome(n) else "false")
```

## JavaScript Solution
```javascript
function isBinaryPalindrome(n) {
  if (n < 0) return false;
  const binary = n.toString(2);
  const reversedBinary = binary.split("").reverse().join("");
  return binary === reversedBinary;
}

const n = parseInt(process.argv[2]);
console.log(isBinaryPalindrome(n));
```