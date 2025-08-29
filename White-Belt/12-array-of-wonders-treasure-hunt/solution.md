# Solutions for Array of Wonders: Treasure Hunt!

### Approach
The solution iterates through the input array using a `for` loop. It counts the number of elements encountered before reaching the element 'X'. The time complexity is O(n), where n is the length of the array, because we iterate through the array once. The space complexity is O(1) as we use a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

int count_before_x(char arr[], int size) {
    int count = 0;
    for (int i = 0; i < size; i++) {
        if (arr[i] == 'X') {
            break;
        }
        count++;
    }
    return count;
}

int main() {
    int n;
    scanf("%d", &n);
    char arr[n];
    for (int i = 0; i < n; i++) {
        scanf(" %c", &arr[i]);
    }
    printf("%d\n", count_before_x(arr, n));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

using namespace std;

int count_before_x(vector<char> &arr) {
    int count = 0;
    for (char c : arr) {
        if (c == 'X') {
            break;
        }
        count++;
    }
    return count;
}

int main() {
    int n;
    cin >> n;
    vector<char> arr(n);
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    cout << count_before_x(arr) << endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class TreasureHunt {

    public static int countBeforeX(char[] arr) {
        int count = 0;
        for (char c : arr) {
            if (c == 'X') {
                break;
            }
            count++;
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        char[] arr = new char[n];
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.next().charAt(0);
        }
        System.out.println(countBeforeX(arr));
        scanner.close();
    }
}
```

## Python Solution
```python
def count_before_x(arr):
    count = 0
    for c in arr:
        if c == 'X':
            break
        count += 1
    return count

n = int(input())
arr = list(input().split())
print(count_before_x(arr))
```

## JavaScript Solution
```javascript
function countBeforeX(arr) {
  let count = 0;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === 'X') {
      break;
    }
    count++;
  }
  return count;
}

const readline = require('readline').createInterface({
    input: process.stdin,
    output: process.stdout,
});

readline.question('Enter the number of elements: ', (n) => {
    readline.question('Enter the array elements separated by spaces: ', (line) => {
        const arr = line.split(' ');
        const result = countBeforeX(arr);
        console.log(result);
        readline.close();
    });
});
```