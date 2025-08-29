# Solutions for Mirror Mirror: Reverse My String!

### Approach
To reverse a string, we can use a simple and efficient technique called the **two-pointer approach**. We'll initialize two pointers: one at the beginning of the string (let's call it `left`) and one at the end of the string (let's call it `right`).
We then enter a loop that continues as long as the `left` pointer is less than the `right` pointer. Inside the loop, we perform the following steps:
1.  **Swap Characters:** Exchange the characters at the `left` and `right` pointer positions.
2.  **Move Pointers:** Increment the `left` pointer and decrement the `right` pointer.
This process effectively swaps characters from the outside in until the pointers meet or cross, at which point the entire string has been reversed.

For languages where strings are immutable (like Java, Python, JavaScript), we first convert the string into a mutable data structure, such as a character array or a list of characters, perform the swaps, and then convert it back into a string. For languages like C or C++ using character arrays, the reversal can often be done directly in-place.

**Time Complexity:** The algorithm iterates through approximately half of the string's length (N/2 swaps). Thus, the time complexity is **O(N)**, where N is the length of the string.
**Space Complexity:** If the reversal is done in-place (modifying the original character array/list directly), the space complexity is **O(1)** (constant extra space). If the string needs to be converted to a new mutable structure and then back to a string (due to language specific string immutability), the space complexity will be **O(N)** to store this temporary structure.

## C Solution
```c
#include <stdio.h>
#include <string.h>

// Function to reverse a string in-place
void reverseString(char* s) {
    int length = strlen(s);
    int i = 0;
    int j = length - 1;
    while (i < j) {
        // Swap characters
        char temp = s[i];
        s[i] = s[j];
        s[j] = temp;
        // Move pointers inward
        i++;
        j--;
    }
}

int main() {
    char inputBuffer[1002]; // Max 1000 chars + newline + null terminator
    
    // Read input string from stdin
    // Using fgets for safer input handling
    if (fgets(inputBuffer, sizeof(inputBuffer), stdin) != NULL) {
        // Remove trailing newline character if present
        inputBuffer[strcspn(inputBuffer, "\n")] = 0;
        
        // Call the core logic function
        reverseString(inputBuffer);
        
        // Print the reversed string
        printf("%s\n", inputBuffer);
    }
    
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <algorithm> // Not strictly needed for manual two-pointer, but useful for std::reverse

// Function to reverse a string
std::string reverseString(std::string s) {
    // For C++, std::string can be directly modified using indices
    // or converted to a char array, but direct modification is common.
    int n = s.length();
    int i = 0;
    int j = n - 1;
    while (i < j) {
        // Swap characters
        char temp = s[i];
        s[i] = s[j];
        s[j] = temp;
        // Move pointers inward
        i++;
        j--;
    }
    return s;
}

int main() {
    std::string inputLine;
    
    // Read input string from stdin
    std::getline(std::cin, inputLine);
    
    // Call the core logic function
    std::string reversedLine = reverseString(inputLine);
    
    // Print the reversed string
    std::cout << reversedLine << std::endl;
    
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to reverse a string
    public String reverseString(String s) {
        // Convert the string to a character array for easier manipulation
        // Strings are immutable in Java, so we need a mutable structure.
        char[] charArray = s.toCharArray();
        
        int i = 0;
        int j = charArray.length - 1;
        
        while (i < j) {
            // Swap characters
            char temp = charArray[i];
            charArray[i] = charArray[j];
            charArray[j] = temp;
            
            // Move pointers inward
            i++;
            j--;
        }
        
        // Convert the character array back to a string
        return new String(charArray);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Read input string from stdin
        String inputLine = scanner.nextLine();
        
        // Create an instance of the Solution class to call the non-static method
        Solution sol = new Solution();
        
        // Call the core logic function
        String reversedLine = sol.reverseString(inputLine);
        
        // Print the reversed string
        System.out.println(reversedLine);
        
        scanner.close();
    }
}
```

## Python Solution
```python
def reverse_string(s: str) -> str:
    # Convert string to a list of characters for mutability
    # Strings are immutable in Python, so we need a mutable structure.
    char_list = list(s)
    
    i = 0
    j = len(char_list) - 1
    
    while i < j:
        # Swap characters
        char_list[i], char_list[j] = char_list[j], char_list[i]
        
        # Move pointers inward
        i += 1
        j -= 1
        
    # Join the list of characters back into a string
    return "".join(char_list)

if __name__ == "__main__":
    # Read input string from stdin
    input_line = input()
    
    # Call the core logic function
    reversed_line = reverse_string(input_line)
    
    # Print the reversed string
    print(reversed_line)
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Function to reverse a string
function reverseString(s) {
    // Convert the string to an array of characters for mutability
    // Strings are immutable in JavaScript, so we need a mutable structure.
    let charArray = s.split('');
    
    let i = 0;
    let j = charArray.length - 1;
    
    while (i < j) {
        // Swap characters
        let temp = charArray[i];
        charArray[i] = charArray[j];
        charArray[j] = temp;
        
        // Move pointers inward
        i++;
        j--;
    }
    
    // Join the array of characters back into a string
    return charArray.join('');
}

rl.on('line', (inputLine) => {
    // Call the core logic function
    let reversedLine = reverseString(inputLine);
    
    // Print the reversed string
    console.log(reversedLine);
    
    rl.close(); // Close the readline interface after processing one line
});
```