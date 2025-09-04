# Solutions for Lexical Shuffle

### Approach
The most efficient way to determine if two strings are anagrams is by using frequency counting. The core idea is that two strings are anagrams if and only if they have the same characters with the same frequencies. We can achieve this by using a frequency array (since the input strings are constrained to lowercase English letters). First, check if the lengths of the two strings are equal; if not, they cannot be anagrams. Then, initialize an integer array of size 26 (representing 'a' through 'z') with all zeros. Iterate through the first string (`s1`), incrementing the count for each character encountered in the frequency array (e.g., `freq[char - 'a']++`). Next, iterate through the second string (`s2`), decrementing the count for each character encountered (`freq[char - 'a']--`). After processing both strings, iterate through the frequency array. If all counts in the array are zero, it means every character in `s1` had a corresponding character in `s2`, and vice versa, indicating they are anagrams. If any count is non-zero, they are not anagrams. This approach utilizes an array for frequency counting, which acts like a simple hash map. The time complexity is O(N) where N is the length of the strings, as we iterate through each string a constant number of times. The space complexity is O(1) because the frequency array size is fixed at 26, independent of the input string length.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>

// Core logic function
bool areAnagrams(const char* s1, const char* s2) {
    int len1 = strlen(s1);
    int len2 = strlen(s2);

    if (len1 != len2) {
        return false;
    }

    int freq[26] = {0}; // Initialize all counts to 0

    // Count characters in s1
    for (int i = 0; i < len1; i++) {
        freq[s1[i] - 'a']++;
    }

    // Decrement counts for characters in s2
    for (int i = 0; i < len2; i++) {
        freq[s2[i] - 'a']--;
    }

    // Check if all counts are zero
    for (int i = 0; i < 26; i++) {
        if (freq[i] != 0) {
            return false;
        }
    }

    return true;
}

int main() {
    char s1[1001]; // Max length 1000 + null terminator
    char s2[1001];

    // Read input strings
    if (scanf("%s", s1) != 1) return 1;
    if (scanf("%s", s2) != 1) return 1;

    // Call the core logic function
    bool result = areAnagrams(s1, s2);

    // Print the result
    if (result) {
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
#include <numeric>

// Core logic function
bool areAnagrams(const std::string& s1, const std::string& s2) {
    if (s1.length() != s2.length()) {
        return false;
    }

    std::vector<int> freq(26, 0); // Initialize all counts to 0

    // Count characters in s1
    for (char c : s1) {
        freq[c - 'a']++;
    }

    // Decrement counts for characters in s2
    for (char c : s2) {
        freq[c - 'a']--;
    }

    // Check if all counts are zero
    for (int count : freq) {
        if (count != 0) {
            return false;
        }
    }

    return true;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    std::string s1, s2;

    // Read input strings
    std::cin >> s1 >> s2;

    // Call the core logic function
    bool result = areAnagrams(s1, s2);

    // Print the result
    if (result) {
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

    // Core logic function
    public boolean areAnagrams(String s1, String s2) {
        if (s1.length() != s2.length()) {
            return false;
        }

        int[] freq = new int[26]; // All elements initialized to 0 by default

        // Count characters in s1
        for (char c : s1.toCharArray()) {
            freq[c - 'a']++;
        }

        // Decrement counts for characters in s2
        for (char c : s2.toCharArray()) {
            freq[c - 'a']--;
        }

        // Check if all counts are zero
        for (int count : freq) {
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

        // Create an instance of the Solution class to call the non-static method
        Solution sol = new Solution();
        boolean result = sol.areAnagrams(s1, s2);

        // Print the result
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

def areAnagrams(s1: str, s2: str) -> bool:
    if len(s1) != len(s2):
        return False

    freq = [0] * 26 # Initialize all counts to 0

    # Count characters in s1
    for char_code in map(ord, s1):
        freq[char_code - ord('a')] += 1

    # Decrement counts for characters in s2
    for char_code in map(ord, s2):
        freq[char_code - ord('a')] -= 1

    # Check if all counts are zero
    for count in freq:
        if count != 0:
            return False

    return True

if __name__ == "__main__":
    # Read input strings from stdin
    s1 = sys.stdin.readline().strip()
    s2 = sys.stdin.readline().strip()

    # Call the core logic function
    result = areAnagrams(s1, s2)

    # Print the result as lowercase 'true' or 'false'
    print(str(result).lower())
```

## JavaScript Solution
```javascript
// Core logic function
function areAnagrams(s1, s2) {
    if (s1.length !== s2.length) {
        return false;
    }

    const freq = new Array(26).fill(0); // Initialize all counts to 0

    // Count characters in s1
    for (let i = 0; i < s1.length; i++) {
        freq[s1.charCodeAt(i) - 'a'.charCodeAt(0)]++;
    }

    // Decrement counts for characters in s2
    for (let i = 0; i < s2.length; i++) {
        freq[s2.charCodeAt(i) - 'a'.charCodeAt(0)]--;
    }

    // Check if all counts are zero
    for (let i = 0; i < freq.length; i++) {
        if (freq[i] !== 0) {
            return false;
        }
    }

    return true;
}

// Main function to handle I/O
function main() {
    // Node.js specific way to read input from stdin
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let lines = [];
    rl.on('line', (line) => {
        lines.push(line);
    });

    rl.on('close', () => {
        const s1 = lines[0];
        const s2 = lines[1];

        // Call the core logic function
        const result = areAnagrams(s1, s2);

        // Print the result
        console.log(result);
    });
}

main();
```