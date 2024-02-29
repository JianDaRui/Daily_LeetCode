### 题目描述

`简单` `二分`

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

给你一个可能存在 重复 元素值的数组 numbers，它原来是一个升序排列的数组，并按上述情形进行了一次旋转。请返回旋转数组的最小元素。例如，数组 [3, 4, 5, 1, 2] 为 [1, 2, 3, 4, 5] 的一次旋转，该数组的最小值为 1。

注意，数组 [a[0], a[1], a[2], ..., a[n-1]] 旋转一次 的结果为数组 [a[n-1], a[0], a[1], a[2], ..., a[n-2]]。

示例 1：

输入：numbers = [3, 4, 5, 1, 2]

输出：1
示例 2：

输入：numbers = [2, 2, 2, 0, 1]

输出：0
提示：

numbers 原来是一个升序排序的数组，并进行了 1 至 n 次旋转

---

思路分析

- 通过读题可以知道，数组本身是一个 **有序数组**，再将其旋转后数组变为 **部分有序**。
- 而这个题目的要求是要寻找数组中最小值。
- **[二分法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95)** 就是用来在有序数组中查找某一特定元素的搜索算法。
- 本地的重点在于寻找旋转点。
- 以 `l` 表示开始索引，以 `r` 表示结束索引，以 `m` 表示中间索引。
- 以 m 为中点，将数组划分为左右区间。
- 如果 nums[m] > nums[r]，说明左侧为有序区间由小变大，旋转点在右侧区间，l = m + 1。
- 如果 nums[m] < nums[r]，说明右侧为有序区间，旋转点在左侧区间，r = m。
- 如果 nums[m] === nums[r]，这时无法判断左右区间那个为有序区间，将 r--。
  - 以 [2, 2, 2, 2, 2, 2, 2] 为例，nums[3] === nums[6]。
  - 需要缩短右区间来逐步查找旋转点。

代码：

- Java

```Java
class Solution {
  public int minArray(int[] nums) {
    int l = 0;
    int r = nums.length - 1;
    while(l < r) {
        int m = l + r >> 1;
        if(nums[m] > nums[r]) {
            l = m + 1;
        } else if(nums[m] < nums[r]) {
            r = m;
        } else {
            r--;
        }
    }
    return nums[l];
  }
}
```

- Python

```Python
class Solution:
  def minArray(self, nums):
    l, r = 0, len(nums) - 1
    while(l < r):
      m = (l + r) >> 1
      if(nums[m] > nums[r]):
        l = m + 1
      elif(nums[m] < nums[r]):
        r = m
      else:
        r -= 1
    return nums[l]
```
