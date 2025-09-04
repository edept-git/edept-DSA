### Description
Imagine a circular track with a specific number of positions, labeled from 0 up to `N-1`. You start at position 0. If you take `K` steps clockwise around the track, what will be your final position?

Your task is to write a program that takes the total number of positions `N` and the number of steps `K` as input, and returns the final position.

### Constraints
* `1 <= N <= 1000` (Total number of positions)
* `0 <= K <= 10000` (Number of steps taken)

### Example
#### Input:
N = 5
K = 7

#### Output:
2

#### Explanation:
Starting at position 0:
* 1st step: position 1
* 2nd step: position 2
* 3rd step: position 3
* 4th step: position 4
* 5th step: position 0 (completes a cycle)
* 6th step: position 1
* 7th step: position 2
So, after 7 steps on a track with 5 positions, you land on position 2.

### Concepts Covered
* Modulo Arithmetic
* Basic Integer Operations