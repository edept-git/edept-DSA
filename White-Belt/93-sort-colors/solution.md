# Solutions for Sort Colors

### Approach
This problem can be solved efficiently using a two-pointer approach. We maintain three pointers: `p0`, `p1`, and `p2`.  `p0` points to the beginning of the 0s region, `p1` points to the current element being processed, and `p2` points to the end of the 2s region. We iterate through the array, and if we encounter a 0, we swap it with the element at `p0` and increment both `p0` and `p1`. If we encounter a 1, we increment `p1`. If we encounter a 2, we swap it with the element at `p2` and decrement `p2`. This ensures that the 0s are at the beginning, the 2s are at the end, and the 1s are in the middle.  The time complexity is O(n) and the space complexity is O(1).

## C Solution
```c
void sortColors(int* nums, int numsSize){
    int p0 = 0, p1 = 0, p2 = numsSize - 1;
    while (p1 <= p2) {
        if (nums[p1] == 0) {
            swap(nums[p0++], nums[p1++]);
        } else if (nums[p1] == 1) {
            p1++;
        } else {
            swap(nums[p1], nums[p2--]);
        }
    }
}
void swap(int *a, int *b){
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

## C++ Solution
```cpp
#include <vector>
void sortColors(std::vector<int>& nums) {
    int p0 = 0, p1 = 0, p2 = nums.size() - 1;
    while (p1 <= p2) {
        if (nums[p1] == 0) {
            std::swap(nums[p0++], nums[p1++]);
        } else if (nums[p1] == 1) {
            p1++;
        } else {
            std::swap(nums[p1], nums[p2--]);
        }
    }
}
```

## Java Solution
```java
class Solution {
    public void sortColors(int[] nums) {
        int p0 = 0, p1 = 0, p2 = nums.length - 1;
        while (p1 <= p2) {
            if (nums[p1] == 0) {
                swap(nums, p0++, p1++);
            } else if (nums[p1] == 1) {
                p1++;
            } else {
                swap(nums, p1, p2--);
            }
        }
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

## Python Solution
```python
def sortColors(nums):
    p0, p1, p2 = 0, 0, len(nums) - 1
    while p1 <= p2:
        if nums[p1] == 0:
            nums[p0], nums[p1] = nums[p1], nums[p0]
            p0 += 1
            p1 += 1
        elif nums[p1] == 1:
            p1 += 1
        else:
            nums[p1], nums[p2] = nums[p2], nums[p1]
            p2 -= 1
```

## JavaScript Solution
```javascript
const sortColors = (nums) => {
    let p0 = 0, p1 = 0, p2 = nums.length - 1;
    while (p1 <= p2) {
        if (nums[p1] === 0) {
            [nums[p0], nums[p1]] = [nums[p1], nums[p0]];
            p0++;
            p1++;
        } else if (nums[p1] === 1) {
            p1++;
        } else {
            [nums[p1], nums[p2]] = [nums[p2], nums[p1]];
            p2--;
        }
    }
};
```