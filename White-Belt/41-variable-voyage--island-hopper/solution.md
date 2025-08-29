# Solutions for Variable Voyage:  Island Hopper

### Approach
The solution uses two integer variables to store the number of islands visited and the total number of coconuts collected. The program takes these values as input from the user using standard input (e.g., `scanf` in C, `cin` in C++, etc.).  The values are then printed to the standard output using formatted output (e.g., `printf` in C, `cout` in C++, etc.). The time and space complexity are both O(1) as we only deal with a fixed number of variables.

## C Solution
```c
#include <stdio.h>

void islandHopper(int islands, int coconuts) {
    printf("Islands Visited: %d, Total Coconuts: %d\n", islands, coconuts);
}

int main() {
    int islands, coconuts;
    scanf("%d %d", &islands, &coconuts);
    islandHopper(islands, coconuts);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

void islandHopper(int islands, int coconuts) {
    std::cout << "Islands Visited: " << islands << ", Total Coconuts: " << coconuts << std::endl;
}

int main() {
    int islands, coconuts;
    std::cin >> islands >> coconuts;
    islandHopper(islands, coconuts);
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class IslandHopper {
    public static void islandHopper(int islands, int coconuts) {
        System.out.println("Islands Visited: " + islands + ", Total Coconuts: " + coconuts);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int islands = scanner.nextInt();
        int coconuts = scanner.nextInt();
        islandHopper(islands, coconuts);
        scanner.close();
    }
}
```

## Python Solution
```python
def islandHopper(islands, coconuts):
    print(f"Islands Visited: {islands}, Total Coconuts: {coconuts}")

if __name__ == "__main__":
    islands, coconuts = map(int, input().split())
    islandHopper(islands, coconuts)
```

## JavaScript Solution
```javascript
function islandHopper(islands, coconuts) {
    console.log(`Islands Visited: ${islands}, Total Coconuts: ${coconuts}`);
}

const input = require('readline-sync').prompt();
let line = input.question();
let [islands, coconuts] = line.split(' ').map(Number);
islandHopper(islands, coconuts);
```