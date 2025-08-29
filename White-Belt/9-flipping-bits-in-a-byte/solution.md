# Solutions for Flipping Bits in a Byte

### Approach
The solution uses the bitwise NOT operator (~) to flip all the bits of the input integer.  The ~ operator inverts each bit in the number.  Since we're working with an 8-bit unsigned integer, we don't need to worry about sign extension. The time complexity is O(1) as it involves a single bitwise operation. The space complexity is also O(1) as we are not using any extra data structures.

## C Solution
```c
#include <stdio.h>
unsigned char flip_bits(unsigned char n) {
  return ~n;
}
int main() {
  unsigned char num;
  scanf("%hhu", &num);
  printf("%hhu\n", flip_bits(num));
  return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
unsigned char flip_bits(unsigned char n) {
  return ~n;
}
int main() {
  unsigned char num;
  std::cin >> num;
  std::cout << (unsigned int)flip_bits(num) << std::endl;
  return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
public class FlipBits {
  public static byte flipBits(byte n) {
    return (byte) ~n;
  }
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    byte num = scanner.nextByte();
    System.out.println(flipBits(num));
    scanner.close();
  }
}
```

## Python Solution
```python
def flip_bits(n):
  return ~n
num = int(input())
print(flip_bits(num) & 0xFF) #Mask to ensure 8-bit output
```

## JavaScript Solution
```javascript
function flipBits(n) {
  return ~n;
}
const num = parseInt(process.argv[2]);
console.log(flipBits(num) >>> 0); // >>> 0 ensures unsigned 32-bit integer
```