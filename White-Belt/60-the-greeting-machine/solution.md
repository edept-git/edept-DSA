# Solutions for The Greeting Machine

### Approach
To solve this problem, we will define a function (let's call it `greetUser`) that accepts one parameter: the user's name. Inside this function, we will use the received name to construct a personalized greeting message. The function will then print this message to the standard output. In the main part of our program, we will first read the user's name from standard input and then pass this name as an argument when calling our `greetUser` function.

**Time Complexity**: O(L), where L is the length of the input name. This is because reading the name and constructing/printing the greeting message will involve operations proportional to its length.
**Space Complexity**: O(L), as we need to store the input name and the constructed greeting string in memory.

## C Solution
```c
#include <stdio.h>
#include <string.h>

// Function to greet a user by name
void greetUser(char* name) {
    printf("Hello, %s! Welcome to the program.\n", name);
}

int main() {
    char name[51]; // Max 50 chars + null terminator

    // Read the user's name from standard input
    // Using fgets to safely read a line including spaces
    if (fgets(name, sizeof(name), stdin) != NULL) {
        // Remove trailing newline character if present
        name[strcspn(name, "\n")] = 0;

        // Call the greetUser function with the input name
        greetUser(name);
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Function to greet a user by name
void greetUser(const std::string& name) {
    std::cout << "Hello, " << name << "! Welcome to the program." << std::endl;
}

int main() {
    std::string name;

    // Read the user's name from standard input
    std::getline(std::cin, name);

    // Call the greetUser function with the input name
    greetUser(name);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to greet a user by name
    public static void greetUser(String name) {
        System.out.println("Hello, " + name + "! Welcome to the program.");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read the user's name from standard input
        String name = scanner.nextLine();

        // Call the greetUser function with the input name
        greetUser(name);

        scanner.close();
    }
}
```

## Python Solution
```python
def greetUser(name):
    """
    Greets a user with a personalized message.
    Args:
        name (str): The name of the user to greet.
    """
    print(f"Hello, {name}! Welcome to the program.")

if __name__ == "__main__":
    # Read the user's name from standard input
    name = input()

    # Call the greetUser function with the input name
    greetUser(name)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to greet a user by name
function greetUser(name) {
    console.log(`Hello, ${name}! Welcome to the program.`);
}

rl.on('line', (line) => {
    // Call the greetUser function with the input name
    greetUser(line);
    rl.close();
});
```