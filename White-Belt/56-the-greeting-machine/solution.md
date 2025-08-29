# Solutions for The Greeting Machine

### Approach
To solve this problem, we will define a function (or method) that takes one parameter: a string representing the person's `name`. Inside this function, we will construct the complete greeting message. The greeting message will start with "Hello, ", then include the provided `name`, and conclude with "! Welcome to DSA!". After forming the complete greeting, this function will return the generated string.

In the main part of our program, we will first read the `name` from the standard input. Then, we will call our greeting generation function, passing the read `name` as an **argument** to its `name` **parameter**. Finally, we will take the string returned by the function and print it to the standard output.

**Time Complexity:** O(L), where L is the length of the input `name`. This is because string concatenation operations typically depend on the length of the strings involved.
**Space Complexity:** O(L), where L is the length of the input `name`. This is due to storing the newly constructed greeting string, which grows with the length of the name.


## C Solution
```c
#include <stdio.h>
#include <string.h> // Required for strcpy, strcat

// Function to generate the greeting message
// It takes the name as input and a buffer to store the greeting
// The bufferSize parameter is crucial to prevent buffer overflows
void generateGreeting(const char* name, char* greetingBuffer, int bufferSize) {
    // Start with the fixed part of the greeting
    strcpy(greetingBuffer, "Hello, ");
    
    // Append the name
    // Ensure not to overflow the buffer; reserve space for null terminator
    strncat(greetingBuffer, name, bufferSize - strlen(greetingBuffer) - 1);
    
    // Append the final part of the greeting
    // Ensure not to overflow the buffer; reserve space for null terminator
    strncat(greetingBuffer, "! Welcome to DSA!", bufferSize - strlen(greetingBuffer) - 1);
}

int main() {
    char name[51]; // Max name length 50 + null terminator
    // Buffer for the greeting: "Hello, " (7) + name (50) + "! Welcome to DSA!" (19) + null (1) = 77
    // A size of 100 is safe.
    char greeting[100]; 
    
    // Read the name from standard input
    // %50s ensures we read at most 50 characters, preventing buffer overflow into 'name'
    scanf("%50s", name);
    
    // Call the logic function to generate the greeting
    generateGreeting(name, greeting, sizeof(greeting));
    
    // Print the generated greeting to standard output
    printf("%s\n", greeting);
    
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Function to generate the greeting message
// Takes a const reference to a string for efficiency and prevents modification
std::string createGreeting(const std::string& name) {
    // Use string concatenation to build the greeting
    std::string greeting = "Hello, ";
    greeting += name;
    greeting += "! Welcome to DSA!";
    return greeting;
}

int main() {
    std::string name;
    
    // Read the name from standard input
    // std::cin >> name reads a single word (whitespace-separated)
    std::cin >> name;
    
    // Call the logic function to generate the greeting
    std::string fullGreeting = createGreeting(name);
    
    // Print the generated greeting to standard output
    std::cout << fullGreeting << std::endl;
    
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class GreetingMachine {

    // Function to generate the greeting message
    // Takes a String name as input and returns the generated greeting
    public static String createGreeting(String name) {
        // Use string concatenation to build the greeting
        String greeting = "Hello, " + name + "! Welcome to DSA!";
        return greeting;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Read the name from standard input
        // .next() reads a single word (up to the next whitespace character)
        String name = scanner.next();
        
        // Call the logic function to generate the greeting
        String fullGreeting = createGreeting(name);
        
        // Print the generated greeting to standard output
        System.out.println(fullGreeting);
        
        // Close the scanner to release system resources
        scanner.close();
    }
}
```

## Python Solution
```python
def create_greeting(name):
    """
    Function to generate the greeting message.
    Takes a string name as input and returns the generated greeting.
    """
    # Use f-strings for easy string formatting and concatenation (Python 3.6+)
    greeting = f"Hello, {name}! Welcome to DSA!"
    return greeting

if __name__ == "__main__":
    # Read the name from standard input
    # input() reads a line from stdin as a string
    name = input()
    
    # Call the logic function to generate the greeting
    full_greeting = create_greeting(name)
    
    # Print the generated greeting to standard output
    print(full_greeting)
```

## JavaScript Solution
```javascript
// Function to generate the greeting message
// Takes a string name as input and returns the generated greeting
function createGreeting(name) {
    // Use template literals (backticks ``) for easy string formatting and concatenation
    const greeting = `Hello, ${name}! Welcome to DSA!`;
    return greeting;
}

// In a typical competitive programming environment in Node.js, 
// input is read synchronously from /dev/stdin.
// .trim() removes any leading/trailing whitespace, including newline characters.
const input = require('fs').readFileSync('/dev/stdin', 'utf8').trim();

// The input will be the name (a single word)
const name = input;

// Call the logic function to generate the greeting
const fullGreeting = createGreeting(name);

// Print the generated greeting to stdout
console.log(fullGreeting);
```