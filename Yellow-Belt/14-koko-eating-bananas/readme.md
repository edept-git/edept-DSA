### Description
Koko loves to eat bananas. There are `n` piles of bananas, and the `i`-th pile has `piles[i]` bananas. Koko has to eat all the bananas within `h` hours.

Koko decides her eating speed `k` (bananas per hour). Each hour, she chooses one pile and eats `k` bananas from it. If a pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during that hour. She cannot start eating from a different pile in the same hour.

Koko wants to eat all the bananas, but she also wants to be slow enough to avoid suspicion. Your task is to find the minimum integer eating speed `k` such that she can eat all the bananas within `h` hours.

### Constraints
* `1 <= piles.length <= 10^4`
* `1 <= piles[i] <= 10^9`
* `piles.length <= h <= 10^9`

### Example

Input:
piles = [3,6,7,11]
h = 8

Output:
4

Explanation:
If k = 1, total hours = 3 + 6 + 7 + 11 = 27 hours (too slow).
If k = 3, total hours = ceil(3/3) + ceil(6/3) + ceil(7/3) + ceil(11/3) = 1 + 2 + 3 + 4 = 10 hours (too slow).
If k = 4, total hours = ceil(3/4) + ceil(6/4) + ceil(7/4) + ceil(11/4) = 1 + 2 + 2 + 3 = 8 hours (just right).
Since we need the minimum k, 4 is the answer.


### Concepts Covered
*   **Binary Search**: This problem asks for the *minimum* `k` that satisfies a certain condition. The time it takes to eat all bananas is a monotonically decreasing function with respect to `k` (i.e., faster `k` means less time). This property makes it a perfect candidate for binary search on the answer space.
*   **Ceiling Division**: When calculating the time taken to eat a pile of `p` bananas at speed `k`, if `p` is not perfectly divisible by `k`, Koko still spends a full hour on the remaining bananas. This is equivalent to `ceil(p / k)`. In integer arithmetic, `ceil(a / b)` can be calculated as `(a + b - 1) / b` for positive integers `a` and `b`.
*   **Time Complexity Analysis**: Understanding how to calculate the overall time taken for an algorithm, considering the number of operations.
*   **Space Complexity Analysis**: Understanding the memory usage of an algorithm, excluding the input storage.
