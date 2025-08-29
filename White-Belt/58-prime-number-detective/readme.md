### Description
A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself. In other words, a prime number has exactly two distinct positive divisors: 1 and the number itself.

Your task is to write a program that takes an integer `N` as input and determines whether it is a prime number. The program should output "true" if `N` is prime, and "false" otherwise.

### Constraints
- `0 <= N <= 1,000,000`

### Example
**Input:**
7

**Output:**
true

**Explanation:**
7 is only divisible by 1 and 7. Since it has exactly two distinct positive divisors, it is a prime number.

**Input:**
4

**Output:**
false

**Explanation:**
4 is divisible by 1, 2, and 4. Since it has a divisor other than 1 and itself (which is 2), it's not a prime number.

**Input:**
1

**Output:**
false

**Explanation:**
By definition, prime numbers must be greater than 1. Therefore, 1 is not a prime number.

### Concepts Covered
- Definition of a Prime Number
- Conditional Statements (if/else)
- Loops (for/while)
- Basic Arithmetic Operations (modulo operator `%`)
- Boolean Logic