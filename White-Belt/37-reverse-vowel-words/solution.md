# Solutions for Reverse Vowel Words

### Approach
The solution involves splitting the input string into words.  Each word is checked for vowels. If a word contains at least one vowel, it's reversed.  The reversed vowel words are then joined back together with spaces to form the output string.  The time complexity is O(n), where n is the length of the string, due to iterating through the string and words. The space complexity is O(n) in the worst case, if all words are vowel words and the reversed words consume significant space.

## C Solution
```c
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int is_vowel(char c) {
    return (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u');
}

void reverse_vowel_words(char *str) {
    char *word = strtok(str, " ");
    char reversed_word[100];
    while (word != NULL) {
        int has_vowel = 0;
        for (int i = 0; word[i]; i++) {
            if (is_vowel(word[i])) {
                has_vowel = 1;
                break;
            }
        }
        if (has_vowel) {
            int len = strlen(word);
            for (int i = 0; i < len; i++) {
                reversed_word[i] = word[len - 1 - i];
            }
            reversed_word[len] = '\0';
            printf("%s ", reversed_word);
        } else {
            printf("%s ", word);
        }
        word = strtok(NULL, " ");
    }
}

int main() {
    char str[1000];
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = 0; //remove trailing newline
    reverse_vowel_words(str);
    printf("\n");
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <algorithm>

bool is_vowel(char c) {
    return (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u');
}

std::string reverse_vowel_words(std::string str) {
    std::string word;
    std::string result = "";
    for (int i = 0; i < str.length(); ++i) {
        if (str[i] == ' ') {
            bool has_vowel = false;
            for (char c : word) {
                if (is_vowel(c)) {
                    has_vowel = true;
                    break;
                }
            }
            if (has_vowel) {
                std::reverse(word.begin(), word.end());
            }
            result += word + " ";
            word = "";
        } else {
            word += str[i];
        }
    }
    bool has_vowel = false;
    for (char c : word) {
        if (is_vowel(c)) {
            has_vowel = true;
            break;
        }
    }
    if (has_vowel) {
        std::reverse(word.begin(), word.end());
    }
    result += word;
    return result;
}

int main() {
    std::string str;
    std::getline(std::cin, str);
    std::cout << reverse_vowel_words(str) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.*;

class Solution {
    boolean isVowel(char c) {
        return "aeiou".indexOf(c) != -1;
    }

    String reverseVowelWords(String str) {
        String[] words = str.split(" ");
        StringBuilder sb = new StringBuilder();
        for (String word : words) {
            boolean hasVowel = false;
            for (char c : word.toCharArray()) {
                if (isVowel(c)) {
                    hasVowel = true;
                    break;
                }
            }
            if (hasVowel) {
                sb.append(new StringBuilder(word).reverse().toString()).append(" ");
            } else {
                sb.append(word).append(" ");
            }
        }
        return sb.toString().trim();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String str = scanner.nextLine();
        Solution sol = new Solution();
        System.out.println(sol.reverseVowelWords(str));
        scanner.close();
    }
}
```

## Python Solution
```python
def is_vowel(c):
    return c in 'aeiou'

def reverse_vowel_words(s):
    words = s.split()
    result = []
    for word in words:
        has_vowel = False
        for c in word:
            if is_vowel(c):
                has_vowel = True
                break
        if has_vowel:
            result.append(word[::-1])
        else:
            result.append(word)
    return ' '.join(result)

if __name__ == "__main__":
    s = input()
    print(reverse_vowel_words(s))
```

## JavaScript Solution
```javascript
function isVowel(c) {
  return "aeiou".includes(c);
}

function reverseVowelWords(str) {
  const words = str.split(" ");
  let result = "";
  for (const word of words) {
    let hasVowel = false;
    for (const c of word) {
      if (isVowel(c)) {
        hasVowel = true;
        break;
      }
    }
    if (hasVowel) {
      result += word.split("").reverse().join("") + " ";
    } else {
      result += word + " ";
    }
  }
  return result.trim();
}

const str = require('readline-sync').prompt().trim();
console.log(reverseVowelWords(str));
```