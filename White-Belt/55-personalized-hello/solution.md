# Solutions for Personalized Hello

### Approach
The core of this problem involves standard input and output operations. We will first declare two variables: one to store the user's name (which will be a string type) and another to store their age (an integer type). The program will then read the name using an input function suitable for strings in the chosen programming language. Immediately after, it will read the age using an input function suitable for integers. Finally, it will construct the greeting message using string concatenation or a formatted print function, combining the literal "Hello ", the stored name, the literal "! You are ", the stored age, and the literal " years old." This entire message will then be printed to standard output. The time complexity will be O(1) as it involves a fixed number of I/O operations and string manipulations. The space complexity will also be O(1) as it only requires a constant amount of memory to store the name and age variables.

## C Solution
```c
#include <stdio.h>

// Function to generate and print the greeting
void greetUser(char name[], int age) {
    printf("Hello %s! You are %d years old.\n", name, age);
}

int main() {
    char name[101]; // Assuming max name length 100 + null terminator
    int age;

    // Read name, limiting to 100 characters to prevent buffer overflow
    scanf("%100s", name);

    // Read age
    scanf("%d", &age);

    // Call the core logic function
    greetUser(name, age);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Function to generate and print the greeting
void greetUser(const std::string& name, int age) {
    std::cout << "Hello " << name << "! You are " << age << " years old." << std::endl;
}

int main() {
    std::string name;
    int age;

    // Read name
    std::cin >> name;

    // Read age
    std::cin >> age;

    // Call the core logic function
    greetUser(name, age);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Main {

    // Function to generate and print the greeting
    public static void greetUser(String name, int age) {
        System.out.println("Hello " + name + "! You are " + age + " years old.");
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read name
        String name = scanner.next();

        // Read age
        int age = scanner.nextInt();

        // Call the core logic function
        greetUser(name, age);

        scanner.close();
    }
}
```

## Python Solution
```python
# Function to generate and print the greeting
def greet_user(name, age):
    print(f"Hello {name}! You are {age} years old.")

def main():
    # Read name
    name = input()

    # Read age
    age = int(input())

    # Call the core logic function
    greet_user(name, age)

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to generate and print the greeting
function greetUser(name, age) {
    console.log(`Hello ${name}! You are ${age} years old.`);
}

let inputs = [];

rl.on('line', (line) => {
    inputs.push(line);
});

rl.on('close', () => {
    // This block acts as the 'main' function after all input is received
    const name = inputs[0];
    const age = parseInt(inputs[1]);

    greetUser(name, age);
});
```