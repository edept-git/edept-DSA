# Solutions for Letter Lockup: Anagram Test

### Approach
The most efficient way to check if two strings are anagrams is by using frequency counting. First, we must ensure that both strings have the same length; if not, they cannot be anagrams. If their lengths are equal, we can proceed. We will use an array (or a hash map) of size 26 to store the frequency of each lowercase English letter, as there are 26 letters from 'a' to 'z'. We iterate through the first string `s`, incrementing the count for each character encountered in our frequency array. Then, we iterate through the second string `t`, decrementing the count for each character. For each character `c` in string `t`, we decrement its corresponding count in the frequency array. If at any point, the count for `c` becomes negative, it means `t` contains more instances of `c` than `s` does, or `t` contains a character not present in `s`, so they cannot be anagrams, and we immediately return `false`. If we successfully iterate through `t` without any count becoming negative, it implies that all characters in `t` were present in `s` with at least the required frequency. Since we already checked that the string lengths are equal, this also implicitly guarantees that all counts in our frequency array must be zero after processing `t`. Therefore, if we complete the second loop, `t` is an anagram of `s`, and we return `true`.

**Time Complexity**: O(N), where N is the length of the strings. We iterate through each string once.
**Space Complexity**: O(1), as we use a fixed-size array of 26 integers, regardless of the input string length.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

#define MAX_STR_LEN 50000

bool isAnagram(char *s, char *t) {
    int len_s = strlen(s);
    int len_t = strlen(t);

    if (len_s != len_t) {
        return false;
    }

    int freq[26];
    memset(freq, 0, sizeof(freq));

    for (int i = 0; i < len_s; i++) {
        freq[s[i] - 'a']++;
    }

    for (int i = 0; i < len_t; i++) {
        freq[t[i] - 'a']--;
        if (freq[t[i] - 'a'] < 0) {
            return false;
        }
    }

    return true;
}

int main() {
    char *s = (char *)malloc(sizeof(char) * (MAX_STR_LEN + 1));
    char *t = (char *)malloc(sizeof(char) * (MAX_STR_LEN + 1));

    if (s == NULL || t == NULL) {
        fprintf(stderr, "Memory allocation failed.\n");
        return 1;
    }

    // Read input strings, limit characters to prevent buffer overflow
    if (scanf("%50000s", s) != 1) {
        fprintf(stderr, "Error reading string s.\n");
        free(s);
        free(t);
        return 1;
    }
    if (scanf("%50000s", t) != 1) {
        fprintf(stderr, "Error reading string t.\n");
        free(s);
        free(t);
        return 1;
    }

    if (isAnagram(s, t)) {
        printf("true\n");
    } else {
        printf("false\n");
    }

    free(s);
    free(t);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <numeric>

class Solution {
public:
    bool isAnagram(std::string s, std::string t) {
        if (s.length() != t.length()) {
            return false;
        }

        std::vector<int> freq(26, 0);

        for (char c : s) {
            freq[c - 'a']++;
        }

        for (char c : t) {
            freq[c - 'a']--;
            if (freq[c - 'a'] < 0) {
                return false;
            }
        }

        return true;
    }
};

int main() {
    std::string s, t;
    std::cin >> s >> t;

    Solution sol;
    if (sol.isAnagram(s, t)) {
        std::cout << "true" << std::endl;
    } else {
        std::cout << "false" << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        int[] freq = new int[26];

        for (char c : s.toCharArray()) {
            freq[c - 'a']++;
        }

        for (char c : t.toCharArray()) {
            freq[c - 'a']--;
            if (freq[c - 'a'] < 0) {
                return false;
            }
        }

        return true;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.next();
        String t = scanner.next();
        scanner.close();

        Solution sol = new Solution();
        if (sol.isAnagram(s, t)) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
    }
}
```

## Python Solution
```python
import sys

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        freq = [0] * 26

        for char_s in s:
            freq[ord(char_s) - ord('a')] += 1

        for char_t in t:
            freq[ord(char_t) - ord('a')] -= 1
            if freq[ord(char_t) - ord('a')] < 0:
                return False
        
        return True

if __name__ == '__main__':
    input_lines = sys.stdin.readlines()
    s = input_lines[0].strip()
    t = input_lines[1].strip()

    sol = Solution()
    if sol.isAnagram(s, t):
        print("true")
    else:
        print("false")
```

## JavaScript Solution
```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    if (s.length !== t.length) {
        return false;
    }

    let freq = new Array(26).fill(0);

    for (let i = 0; i < s.length; i++) {
        freq[s.charCodeAt(i) - 'a'.charCodeAt(0)]++;
    }

    for (let i = 0; i < t.length; i++) {
        freq[t.charCodeAt(i) - 'a'.charCodeAt(0)]--;
        if (freq[t.charCodeAt(i) - 'a'.charCodeAt(0)] < 0) {
            return false;
        }
    }

    return true;
};

// Main function for handling input/output in a Node.js-like environment
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
  const s = lines[0];
  const t = lines[1];

  if (isAnagram(s, t)) {
    console.log("true");
  } else {
    console.log("false");
  }
});
```