### Description
You are given a string `s` consisting solely of the following characters: '(', ')', '{', '}', '[', ']'.
Determine if the input string is valid. An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### Constraints
*   `1 <= s.length <= 10^4`
*   `s` consists only of '(', ')', '{', '}', '[', ']'.

### Example
Input: "([{}])"
Output: true

Input: "([)]"
Output: false

### Concepts Covered
*   Stack Data Structure
*   String Manipulation
*   Hash Maps (for bracket matching, in some languages)
*   Edge Case Handling (e.g., empty string, unmatched brackets)