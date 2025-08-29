# Solutions for Array of Wonders: Find the Sum of Even Numbers

### Approach
The solution involves iterating through the input array. For each element, we check if it's even using the modulo operator (%). If it's even, we add it to a running sum.  The time complexity is O(n) where n is the length of the array, as we iterate through each element once. The space complexity is O(1) as we only use a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int sumEvenNumbers(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2 == 0) {
            sum += arr[i];
        }
    }
    return sum;
}

int main() {
    int size, arr[100];
    scanf("%d", &size);
    for (int i = 0; i < size; i++) {
        scanf("%d", &arr[i]);
    }
    int result = sumEvenNumbers(arr, size);
    printf("%d\n", result);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

int sumEvenNumbers(int arr[], int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] % 2 == 0) {
            sum += arr[i];
        }
    }
    return sum;
}

int main() {
    int size; 
    std::cin >> size;
    int arr[100];
    for (int i = 0; i < size; i++) {
        std::cin >> arr[i];
    }
    int result = sumEvenNumbers(arr, size);
    std::cout << result << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Arrays;
import java.util.Scanner;

public class SumEven {

    public static int sumEvenNumbers(int[] arr) {
        int sum = 0;
        for (int num : arr) {
            if (num % 2 == 0) {
                sum += num;
            }
        }
        return sum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int size = scanner.nextInt();
        int[] arr = new int[size];
        for (int i = 0; i < size; i++) {
            arr[i] = scanner.nextInt();
        }
        int result = sumEvenNumbers(arr);
        System.out.println(result);
        scanner.close();
    }
}
```

## Python Solution
```python
def sum_even_numbers(arr):
    sum = 0
    for num in arr:
        if num % 2 == 0:
            sum += num
    return sum

size = int(input())
arr = list(map(int, input().split()))
result = sum_even_numbers(arr)
print(result)
```

## JavaScript Solution
```javascript
function sumEvenNumbers(arr) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 === 0) {
      sum += arr[i];
    }
  }
  return sum;
}

const size = parseInt(readline());
const arr = readline().split(' ').map(Number);
const result = sumEvenNumbers(arr);
print(result);
```