### Description
You are given a string `s` consisting of unique lowercase English letters. Your task is to generate and print all possible permutations of this string. A permutation is an arrangement of all its characters in a different order.

### Constraints
*   `1 <= s.length <= 7` (To keep the number of permutations manageable for a Yellow Belt)
*   `s` consists only of unique lowercase English letters.

### Example
**Input:**

abc


**Output:**

abc
acb
bac
bca
cab
cba


### Concepts Covered
*   **Backtracking:** A general algorithmic technique for finding all (or some) solutions to a computational problem, particularly constraint satisfaction problems, by systematically trying to build a solution incrementally. If a partial solution cannot be completed to a valid solution, it "backtracks" to an earlier state and tries another option.
*   **Recursion:** A function calling itself to solve a smaller instance of the same problem. Backtracking problems are often naturally solved using recursion.
*   **Base Cases:** The condition under which a recursive function stops calling itself and returns a result.
*   **State Management:** Keeping track of the current state of the solution (e.g., characters chosen so far, characters remaining to be chosen) during the recursive calls.
