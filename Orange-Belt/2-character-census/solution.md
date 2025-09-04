# Solutions for Character Census

### Approach
The most efficient way to solve this problem is by using a Hash Map (or a frequency array which acts as a specialized hash map). We can iterate through the input string character by character. For each character encountered, we check if it already exists as a key in our hash map. If it does, we increment its corresponding frequency count. If it doesn't, we add it to the hash map with a frequency count of 1. After iterating through the entire string, the hash map will contain all unique characters and their respective frequencies. Finally, we iterate through the map to print the character-frequency pairs, ensuring they are sorted alphabetically by character.
The time complexity will be O(N) where N is the length of the input string, as we iterate through the string once to populate the hash map. Retrieving and updating counts in a hash map takes average O(1) time. Sorting the output characters (which are at most 26 lowercase English letters) will take O(K log K) where K is the number of unique characters, but since K is a small constant (at most 26), this is effectively O(1).
The space complexity will be O(K) for storing the character frequencies in the hash map. In the worst case, if all characters are unique, K will be the number of unique characters in the string (at most 26 for lowercase English letters). Thus, the space complexity is effectively O(1) because the size of the character set is fixed and small.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

// Function to count character frequencies
void countCharacterFrequencies(const char* s) {
    int frequencies[26] = {0}; // Initialize all counts to 0
    int len = strlen(s);

    // Populate frequencies array
    for (int i = 0; i < len; i++) {
        // The constraint guarantees 'a'-'z', so this check is technically not strictly needed
        // but good for robustness.
        if (s[i] >= 'a' && s[i] <= 'z') {
            frequencies[s[i] - 'a']++;
        }
    }

    // Print frequencies in alphabetical order
    int first_printed = 0;
    for (int i = 0; i < 26; i++) {
        if (frequencies[i] > 0) {
            if (first_printed) {
                printf(", ");
            }
            printf("%c:%d", (char)('a' + i), frequencies[i]);
            first_printed = 1;
        }
    }
    printf("\n");
}

int main() {
    char s[1001]; // Max length 1000 + null terminator

    // Read input string
    if (fgets(s, sizeof(s), stdin) != NULL) {
        // Remove trailing newline character if present
        s[strcspn(s, "\n")] = 0;
        countCharacterFrequencies(s);
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <map>

// Function to count character frequencies
void countCharacterFrequencies(const std::string& s) {
    std::map<char, int> frequencies; // std::map keeps keys sorted automatically

    // Populate frequencies map
    for (char c : s) {
        // The constraint guarantees 'a'-'z', so this check is technically not strictly needed
        // but good for robustness.
        if (c >= 'a' && c <= 'z') {
            frequencies[c]++;
        }
    }

    // Print frequencies in alphabetical order
    bool firstPrinted = false;
    for (const auto& pair : frequencies) {
        if (firstPrinted) {
            std::cout << ", ";
        }
        std::cout << pair.first << ":" << pair.second;
        firstPrinted = true;
    }
    std::cout << std::endl;
}

int main() {
    std::string s;
    // Read input string
    std::getline(std::cin, s);

    countCharacterFrequencies(s);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.Map;
import java.util.TreeMap; // TreeMap keeps keys sorted automatically

public class Solution {

    // Function to count character frequencies
    public void countCharacterFrequencies(String s) {
        Map<Character, Integer> frequencies = new TreeMap<>(); // TreeMap automatically sorts by key

        // Populate frequencies map
        for (char c : s.toCharArray()) {
            // The constraint guarantees 'a'-'z', so this check is technically not strictly needed
            // but good for robustness.
            if (c >= 'a' && c <= 'z') {
                frequencies.put(c, frequencies.getOrDefault(c, 0) + 1);
            }
        }

        // Print frequencies in alphabetical order
        StringBuilder result = new StringBuilder();
        boolean firstPrinted = false;
        for (Map.Entry<Character, Integer> entry : frequencies.entrySet()) {
            if (firstPrinted) {
                result.append(", ");
            }
            result.append(entry.getKey()).append(":").append(entry.getValue());
            firstPrinted = true;
        }
        System.out.println(result.toString());
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.nextLine(); // Read input string
        scanner.close();

        Solution sol = new Solution();
        sol.countCharacterFrequencies(s);
    }
}
```

## Python Solution
```python
import sys

def count_character_frequencies(s):
    frequencies = {} # Python dictionary acts as a hash map

    # Populate frequencies dictionary
    for char_code in s:
        # The constraint guarantees 'a'-'z', so this check is technically not strictly needed
        # but good for robustness.
        if 'a' <= char_code <= 'z':
            frequencies[char_code] = frequencies.get(char_code, 0) + 1

    # Sort keys and print frequencies
    sorted_chars = sorted(frequencies.keys())
    
    result_parts = []
    for char_code in sorted_chars:
        result_parts.append(f"{char_code}:{frequencies[char_code]}")
    
    print(", ".join(result_parts))

if __name__ == "__main__":
    s = sys.stdin.readline().strip() # Read input string
    count_character_frequencies(s)
```

## JavaScript Solution
```javascript
function countCharacterFrequencies(s) {
    const frequencies = new Map(); // JavaScript Map acts as a hash map

    // Populate frequencies map
    for (const char of s) {
        // The constraint guarantees 'a'-'z', so this check is technically not strictly needed
        // but good for robustness.
        if (char >= 'a' && char <= 'z') {
            frequencies.set(char, (frequencies.get(char) || 0) + 1);
        }
    }

    // Sort keys and print frequencies
    const sortedChars = Array.from(frequencies.keys()).sort();
    
    const resultParts = [];
    for (const char of sortedChars) {
        resultParts.push(`${char}:${frequencies.get(char)}`);
    }
    
    console.log(resultParts.join(", "));
}

// Read input from stdin
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    countCharacterFrequencies(line);
    rl.close();
});

```