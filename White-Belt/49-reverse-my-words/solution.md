# Solutions for Reverse My Words!

### Approach
This problem can be solved by splitting the input string into an array of words using spaces as delimiters. Then, we reverse the array of words and join them back into a string with single space separation. The time complexity is O(n), where n is the length of the string, as we iterate through the string once for splitting and once for joining. The space complexity is O(n) in the worst case, as we create an array of words that can be the same size as the input string. 

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* reverseWords(char *s) {
    char *word = strtok(s, " ");
    char **words = malloc(sizeof(char*) * strlen(s));
    int i = 0;
    while (word != NULL) {
        words[i++] = word;
        word = strtok(NULL, " ");
    }

    for (int j = 0; j < i / 2; j++) {
        char *temp = words[j];
        words[j] = words[i - 1 - j];
        words[i - 1 - j] = temp;
    }

    char *reversed = malloc(strlen(s) + 1);
    strcpy(reversed, words[0]);
    for (int j = 1; j < i; j++) {
        strcat(reversed, " ");
        strcat(reversed, words[j]);
    }
    free(words);
    return reversed;
}

int main() {
    char s[100];
    fgets(s, sizeof(s), stdin);
    s[strcspn(s, "\n")] = 0;
    char *reversed = reverseWords(strdup(s));
    printf("%s\n", reversed);
    free(reversed);
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

std::string reverseWords(std::string s) {
    std::vector<std::string> words;
    std::string word;
    for (char c : s) {
        if (c == ' ') {
            if (!word.empty()) {
                words.push_back(word);
                word = "";
            }
        } else {
            word += c;
        }
    }
    if (!word.empty()) {
        words.push_back(word);
    }
    std::reverse(words.begin(), words.end());
    std::string result = "";
    for (size_t i = 0; i < words.size(); ++i) {
        result += words[i];
        if (i < words.size() - 1) {
            result += " ";
        }
    }
    return result;
}

int main() {
    std::string s;
    std::getline(std::cin, s);
    std::cout << reverseWords(s) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.*;

public class ReverseWords {
    public static String reverseWords(String s) {
        String[] words = s.trim().split(" + ");
        Collections.reverse(Arrays.asList(words));
        return String.join(" ", words);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.nextLine();
        System.out.println(reverseWords(s));
        scanner.close();
    }
}
```

## Python Solution
```python
def reverse_words(s):
    words = s.split()
    words.reverse()
    return " ".join(words)

s = input()
print(reverse_words(s))
```

## JavaScript Solution
```javascript
function reverseWords(s) {
  const words = s.trim().split(/\s+/);
  words.reverse();
  return words.join(' ');
}

const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question('', (s) => {
  console.log(reverseWords(s));
  readline.close();
});
```