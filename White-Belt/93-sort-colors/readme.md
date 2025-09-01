# Sort Colors

Given an array `nums` with `n` objects colored red, white, or blue, sort them **in-place** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

**You must solve this problem without using the library's sort function.**

**Example 1:**


Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]


**Example 2:**


Input: nums = [2,0,1]
Output: [0,1,2]


**Example 3:**


Input: nums = [0]
Output: [0]


**Example 4:**


Input: nums = [1]
Output: [1]


**Constraints:**

* `n == nums.length`
* `1 <= n <= 300`
* `nums[i]` is either 0, 1, or 2.

**Follow up:** Could you come up with a one-pass algorithm using only constant extra space?

### Concepts Covered

* **In-place sorting:**  Sorting an array without using extra space proportional to the input size. This often involves clever manipulation of array indices.
* **Two-pointer approach:** Using multiple pointers to track different sections of the array simultaneously.  This is very efficient for problems like this where you can partition the array based on the values.
* **Counting sort (implicitly):** While not explicitly implemented as a counting sort, the logic implicitly counts the occurrences of 0s, 1s, and 2s to guide the sorting process.  This means the algorithm runs in linear time.  Understanding the concepts underlying counting sort helps visualize the efficiency of this approach.
* **Array manipulation:** Efficiently managing and rearranging array elements using their indices.
