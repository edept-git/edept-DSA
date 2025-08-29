# Solutions for Galactic Greeting Generator

### Approach
The solution uses a function `generateGreeting` that takes the planet name as input and returns the formatted greeting string.  String concatenation is used to combine the planet name with the fixed greeting message. The time complexity is O(n), where n is the length of the planet name (due to string concatenation), and space complexity is O(n) to store the resulting string. 

## C Solution
```c
#include <stdio.h>
#include <string.h>

char* generateGreeting(char* planetName) {
    char greeting[100];
    sprintf(greeting, "Greetings from %s! Welcome to the Galactic Federation.", planetName);
    return greeting;
}

int main() {
    char planetName[50];
    scanf("%s", planetName);
    printf("%s\n", generateGreeting(planetName));
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

std::string generateGreeting(std::string planetName) {
    return "Greetings from " + planetName + "! Welcome to the Galactic Federation.";
}

int main() {
    std::string planetName;
    std::cin >> planetName;
    std::cout << generateGreeting(planetName) << std::endl;
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class GalacticGreeting {
    public static String generateGreeting(String planetName) {
        return "Greetings from " + planetName + "! Welcome to the Galactic Federation.";
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String planetName = scanner.nextLine();
        System.out.println(generateGreeting(planetName));
        scanner.close();
    }
}
```

## Python Solution
```python
def generateGreeting(planetName):
    return f"Greetings from {planetName}! Welcome to the Galactic Federation."

planetName = input()
print(generateGreeting(planetName))
```

## JavaScript Solution
```javascript
function generateGreeting(planetName) {
  return `Greetings from ${planetName}! Welcome to the Galactic Federation.`;
}

const planetName = require('readline-sync').question();
console.log(generateGreeting(planetName));
```