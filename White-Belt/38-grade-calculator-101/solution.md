# Solutions for Grade Calculator 101

### Approach
The solution uses a series of if-else statements to check the input score against the grade boundaries.  The time complexity is O(1) as it involves a constant number of comparisons. The space complexity is also O(1) as it uses a constant amount of extra space.

## C Solution
```c
#include <stdio.h>

char calculateGrade(int score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

int main() {
    int score;
    scanf("%d", &score);
    printf("%c\n", calculateGrade(score));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>

char calculateGrade(int score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

int main() {
    int score;
    std::cin >> score;
    std::cout << calculateGrade(score) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class GradeCalculator {
    public static char calculateGrade(int score) {
        if (score >= 90) {
            return 'A';
        } else if (score >= 80) {
            return 'B';
        } else if (score >= 70) {
            return 'C';
        } else if (score >= 60) {
            return 'D';
        } else {
            return 'F';
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int score = scanner.nextInt();
        System.out.println(calculateGrade(score));
        scanner.close();
    }
}
```

## Python Solution
```python
def calculateGrade(score):
    if score >= 90:
        return 'A'
    elif score >= 80:
        return 'B'
    elif score >= 70:
        return 'C'
    elif score >= 60:
        return 'D'
    else:
        return 'F'

score = int(input())
print(calculateGrade(score))
```

## JavaScript Solution
```javascript
function calculateGrade(score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

let score = parseInt(readline());
print(calculateGrade(score));
```