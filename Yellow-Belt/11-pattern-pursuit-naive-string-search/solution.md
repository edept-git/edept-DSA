# Solutions for Pattern Pursuit: Naive String Search

### Approach
The naive approach iterates through the text. For each character, it compares the subsequent characters with the pattern. If a mismatch occurs, it moves to the next character in the text; otherwise, it records the match index and continues.

## C Solution
```c
c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int* naivePatternSearch(char *text, char *pattern) {
    int textLen = strlen(text);
    int patternLen = strlen(pattern);
    int *matches = (int*)malloc(textLen * sizeof(int));
    int matchCount = 0;

    for (int i = 0; i <= textLen - patternLen; i++) {
        int j;
        for (j = 0; j < patternLen; j++) {
            if (text[i + j] != pattern[j]) {
                break;
            }
        }
        if (j == patternLen) {
            matches[matchCount++] = i;
        }
    }

    matches = (int*)realloc(matches, matchCount * sizeof(int));
    return matches;
}

int main() {
    char text[] = "abcabcabc";
    char pattern[] = "abc";
    int *matches = naivePatternSearch(text, pattern);
    int count = 0; 
    while(matches[count] != 0){ // Assuming 0 signifies end of the array. Consider better end-of-list indication in real-world apps. 
        printf("%d ", matches[count]);
        count++;
    }
    printf("\n");
    free(matches);
    return 0;
}

```

## C++ Solution
```cpp
cpp
#include <iostream>
#include <vector>
#include <string>

std::vector<int> naivePatternSearch(const std::string& text, const std::string& pattern) {
    std::vector<int> matches;
    for (int i = 0; i <= (int)text.length() - (int)pattern.length(); ++i) {
        bool match = true;
        for (int j = 0; j < pattern.length(); ++j) {
            if (text[i + j] != pattern[j]) {
                match = false;
                break;
            }
        }
        if (match) {
            matches.push_back(i);
        }
    }
    return matches;
}

int main() {
    std::string text = "abcabcabc";
    std::string pattern = "abc";
    std::vector<int> matches = naivePatternSearch(text, pattern);
    for (int match : matches) {
        std::cout << match << " ";
    }
    std::cout << std::endl;
    return 0;
}

```

## Java Solution
```java
java
import java.util.ArrayList;
import java.util.List;

public class NaivePatternSearch {

    public static List<Integer> naivePatternSearch(String text, String pattern) {
        List<Integer> matches = new ArrayList<>();
        for (int i = 0; i <= text.length() - pattern.length(); i++) {
            boolean match = true;
            for (int j = 0; j < pattern.length(); j++) {
                if (text.charAt(i + j) != pattern.charAt(j)) {
                    match = false;
                    break;
                }
            }
            if (match) {
                matches.add(i);
            }
        }
        return matches;
    }

    public static void main(String[] args) {
        String text = "abcabcabc";
        String pattern = "abc";
        List<Integer> matches = naivePatternSearch(text, pattern);
        System.out.println(matches);
    }
}

```

## Python Solution
```python
python
def naive_pattern_search(text, pattern):
    matches = []
    for i in range(len(text) - len(pattern) + 1):
        if text[i:i + len(pattern)] == pattern:
            matches.append(i)
    return matches

text = "abcabcabc"
pattern = "abc"
matches = naive_pattern_search(text, pattern)
print(matches)

```

## JavaScript Solution
```javascript
javascript
function naivePatternSearch(text, pattern) {
  const matches = [];
  for (let i = 0; i <= text.length - pattern.length; i++) {
    let match = true;
    for (let j = 0; j < pattern.length; j++) {
      if (text[i + j] !== pattern[j]) {
        match = false;
        break;
      }
    }
    if (match) {
      matches.push(i);
    }
  }
  return matches;
}

const text = "abcabcabc";
const pattern = "abc";
const matches = naivePatternSearch(text, pattern);
console.log(matches);

```