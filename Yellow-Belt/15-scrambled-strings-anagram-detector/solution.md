# Solutions for Scrambled Strings: Anagram Detector

### Approach
To determine if two strings are anagrams, we need to check if they have the same characters with the same frequencies. A straightforward approach involves using a frequency counter. First, compare the lengths of the two strings. If their lengths are different, they cannot be anagrams, and we can immediately return `false`. Otherwise, we can proceed.

We can use an array of size 26 (for the 26 lowercase English letters) to keep track of character counts. Initialize all elements of this array to zero. Then, iterate through the first string: for each character, increment its corresponding count in the frequency array. Next, iterate through the second string: for each character, decrement its corresponding count in the frequency array. 

After processing both strings, iterate through the frequency array. If all counts are zero, it means every character in the first string was perfectly matched by a character in the second string, and vice-versa. In this case, the strings are anagrams, and we return `true`. If any count is non-zero, they are not anagrams.

This approach uses an array as a frequency map, which is very efficient for a fixed small alphabet size. The time complexity will be O(N + M), where N and M are the lengths of the two strings, because we iterate through each string once. Since we first check if N == M, this simplifies to O(N) if we consider N to be the length of both strings. The space complexity is O(1) because the frequency array size is fixed at 26, regardless of the input string lengths.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

#define ALPHABET_SIZE 26

// Function to check if two strings are anagrams
bool areAnagrams(const char* s1, const char* s2) {
    int len1 = strlen(s1);
    int len2 = strlen(s2);

    // If lengths are different, they cannot be anagrams
    if (len1 != len2) {
        return false;
    }

    // Frequency array for lowercase English letters
    int counts[ALPHABET_SIZE] = {0}; // Initialize all to 0

    // Increment counts for characters in s1
    for (int i = 0; i < len1; i++) {
        counts[s1[i] - 'a']++;
    }

    // Decrement counts for characters in s2
    for (int i = 0; i < len2; i++) {
        counts[s2[i] - 'a']--;
    }

    // Check if all counts are zero
    for (int i = 0; i < ALPHABET_SIZE; i++) {
        if (counts[i] != 0) {
            return false;
        }
    }

    return true;
}

int main() {
    char s1_buffer[100001]; // Max length + 1 for null terminator
    char s2_buffer[100001];

    // Read input strings
    if (scanf("%s", s1_buffer) != 1) return 1;
    if (scanf("%s", s2_buffer) != 1) return 1;

    // Call the core logic function
    if (areAnagrams(s1_buffer, s2_buffer)) {
        printf("true\n");
    } else {
        printf("false\n");
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <vector>

// Function to check if two strings are anagrams
bool areAnagrams(const std::string& s1, const std::string& s2) {
    // If lengths are different, they cannot be anagrams
    if (s1.length() != s2.length()) {
        return false;
    }

    // Frequency array for lowercase English letters
    std::vector<int> counts(26, 0); // Initialize all to 0

    // Increment counts for characters in s1
    for (char c : s1) {
        counts[c - 'a']++;
    }

    // Decrement counts for characters in s2
    for (char c : s2) {
        counts[c - 'a']--;
    }

    // Check if all counts are zero
    for (int count : counts) {
        if (count != 0) {
            return false;
        }
    }

    return true;
}

int main() {
    std::ios_base::sync_with_stdio(false); // Optimize C++ I/O
    std::cin.tie(NULL);

    std::string s1, s2;

    // Read input strings
    std::cin >> s1 >> s2;

    // Call the core logic function
    if (areAnagrams(s1, s2)) {
        std::cout << "true\n";
    } else {
        std::cout << "false\n";
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class Solution {

    // Function to check if two strings are anagrams
    public static boolean areAnagrams(String s1, String s2) {
        // If lengths are different, they cannot be anagrams
        if (s1.length() != s2.length()) {
            return false;
        }

        // Frequency array for lowercase English letters
        int[] counts = new int[26]; // Initialize all to 0 by default

        // Increment counts for characters in s1
        for (char c : s1.toCharArray()) {
            counts[c - 'a']++;
        }

        // Decrement counts for characters in s2
        for (char c : s2.toCharArray()) {
            counts[c - 'a']--;
        }

        // Check if all counts are zero
        for (int count : counts) {
            if (count != 0) {
                return false;
            }
        }

        return true;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read input strings
        String s1 = scanner.next();
        String s2 = scanner.next();

        // Call the core logic function
        if (areAnagrams(s1, s2)) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }

        scanner.close();
    }
}
```

## Python Solution
```python
def are_anagrams(s1: str, s2: str) -> bool:
    # If lengths are different, they cannot be anagrams
    if len(s1) != len(s2):
        return False

    # Frequency array (list) for lowercase English letters
    counts = [0] * 26

    # Increment counts for characters in s1
    for char_code in map(ord, s1):
        counts[char_code - ord('a')] += 1

    # Decrement counts for characters in s2
    for char_code in map(ord, s2):
        counts[char_code - ord('a')] -= 1

    # Check if all counts are zero
    for count in counts:
        if count != 0:
            return False

    return True

def main():
    s1 = input()
    s2 = input()

    # Call the core logic function
    if are_anagrams(s1, s2):
        print("true")
    else:
        print("false")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Function to check if two strings are anagrams
function areAnagrams(s1, s2) {
    // If lengths are different, they cannot be anagrams
    if (s1.length !== s2.length) {
        return false;
    }

    // Frequency array for lowercase English letters
    const counts = new Array(26).fill(0);

    // Increment counts for characters in s1
    for (let i = 0; i < s1.length; i++) {
        counts[s1.charCodeAt(i) - 'a'.charCodeAt(0)]++;
    }

    // Decrement counts for characters in s2
    for (let i = 0; i < s2.length; i++) {
        counts[s2.charCodeAt(i) - 'a'.charCodeAt(0)]--;
    }

    // Check if all counts are zero
    for (let i = 0; i < counts.length; i++) {
        if (counts[i] !== 0) {
            return false;
        }
    }

    return true;
}

// Main function to handle I/O
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let lines = [];
    rl.on('line', (line) => {
        lines.push(line);
    }).on('close', () => {
        const s1 = lines[0];
        const s2 = lines[1];

        // Call the core logic function
        if (areAnagrams(s1, s2)) {
            console.log("true");
        } else {
            console.log("false");
        }
    });
}

// Invoke the main function
main();
```