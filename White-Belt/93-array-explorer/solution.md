# Solutions for Array Explorer

### Approach
Iterate through the array using a loop and print each element.

## C Solution
```c
c
#include <stdio.h>

int main() {
  int arr[] = {1, 2, 3, 4, 5};
  int n = sizeof(arr) / sizeof(arr[0]);

  for (int i = 0; i < n; i++) {
    printf("%d ", arr[i]);
  }
  printf("\n");
  return 0;
}

```

## C++ Solution
```cpp
cpp
#include <iostream>
#include <vector>

int main() {
  std::vector<int> arr = {1, 2, 3, 4, 5};

  for (int i = 0; i < arr.size(); i++) {
    std::cout << arr[i] << " ";
  }
  std::cout << std::endl;
  return 0;
}

```

## Java Solution
```java
java
public class ArrayExplorer {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};

        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
        System.out.println();
    }
}

```

## Python Solution
```python
python
arr = [1, 2, 3, 4, 5]

for i in arr:
    print(i, end=" ")
print()
```

## JavaScript Solution
```javascript
javascript
const arr = [1, 2, 3, 4, 5];

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i], " ");
}
console.log();

```