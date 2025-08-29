# Solutions for Array of Wonders: Summing the Digits

### Approach
The solution iterates through each element of the input array. For each element, we convert it to a string (or alternatively, extract digits using modulo and division). Then, we iterate through the digits (characters of the string), convert them back to integers, and accumulate the sum. The final sum is returned.  The time complexity is O(n*k), where n is the length of the array and k is the average number of digits in each integer. Space complexity is O(1) if digit extraction is done without string conversion; otherwise it's O(k) where k is the maximum number of digits in an integer.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int sum_digits_in_array(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        char num_str[10];
        sprintf(num_str, "%d", arr[i]);
        for (int j = 0; j < strlen(num_str); j++) {
            sum += num_str[j] - '0';
        }
    }
    return sum;
}

int main() {
    int arr[] = {12, 4, 87};
    int size = sizeof(arr) / sizeof(arr[0]);
    int result = sum_digits_in_array(arr, size);
    printf("%d\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

using namespace std;

int sum_digits_in_array(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        string num_str = to_string(arr[i]);
        for (char c : num_str) {
            sum += c - '0';
        }
    }
    return sum;
}

int main() {
    int arr[] = {12, 4, 87};
    int size = sizeof(arr) / sizeof(arr[0]);
    int result = sum_digits_in_array(arr, size);
    cout << result << endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;

public class SumDigits {
    public static int sumDigitsInArray(int[] arr) {
        int sum = 0;
        for (int num : arr) {
            String numStr = Integer.toString(num);
            for (int i = 0; i < numStr.length(); i++) {
                sum += Character.getNumericValue(numStr.charAt(i));
            }
        }
        return sum;
    }

    public static void main(String[] args) {
        int[] arr = {12, 4, 87};
        int result = sumDigitsInArray(arr);
        System.out.println(result);
    }
}
```

## Python Solution
```python
def sum_digits_in_array(arr):
    sum = 0
    for num in arr:
        for digit in str(num):
            sum += int(digit)
    return sum

arr = [12, 4, 87]
result = sum_digits_in_array(arr)
print(result)
```

## JavaScript Solution
```javascript
function sumDigitsInArray(arr) {
  let sum = 0;
  for (let num of arr) {
    String(num).split('').forEach(digit => sum += parseInt(digit));
  }
  return sum;
}

let arr = [12, 4, 87];
let result = sumDigitsInArray(arr);
console.log(result);
```