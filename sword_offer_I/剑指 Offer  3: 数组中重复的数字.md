### 题目描述

`中等` `数组` `哈希表`

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 


限制：

2 <= n <= 100000

---

### 原地交换(推荐 ⭐️⭐️⭐️⭐️⭐️)

分析：

- 已经知道数组长度为 n ，数字范围在 0 ~ n - 1 之间，这意味着在理想情况下 `nums[i] === i`。
- 则可以通过下标 `i` 获取 `nums[i]`，如果 `i === nums[i]`，`nums[i]` 在其理想位置，则 `i` 递增遍历下一个元素。
- 如果不是，说明 `nums[i]` 需要交换，通过循环将 `[nums[j], nums[i]] = [nums[i], nums[j]]` 进行交换，直到 `nums[i] === i`。
- 交换之后，`nums[i]` 和下标 `i` 都发生了变化，`i` 递增到下一个元素，`nums[i]` 为理想元素。
- 如果后续还存在 `nums[i] !==  i`，并且 `nums[nums[i]] === nums[i]` 的情况，说明 `nums[nums[i]]` 已经在其理想位置，但 `nums[nums[i]]` 为重复的元素。直接返回

代码：

- javascript
```javascript
function findRepeatNumber(nums) {
  let i = 0;
  while(true) {
    while(nums[i] !== i) {
      const j = nums[i]
      if(j == nums[j]) {
        return j
      }
      [nums[j], nums[i]] = [nums[i], nums[j]]
      console.log(i, j, nums)
    }
    console.log(i, nums)
    i++
  }
}

0 2 [1, 3, 2, 0, 2, 5, 3]
0 1 [3, 1, 2, 0, 2, 5, 3]
0 3 [0, 1, 2, 3, 2, 5, 3]
1 0 [0, 1, 2, 3, 2, 5, 3]
1 1 [0, 1, 2, 3, 2, 5, 3]
1 2 [0, 1, 2, 3, 2, 5, 3]
1 3 [0, 1, 2, 3, 2, 5, 3]

```
- Java
```java
  class Solution {
    public int findRepeatNumber(int[] nums) {
      int i = 0;
      while(true) {
        while(nums[i] != i) {
          int j = nums[i];
          if(j == nums[j]) {
            return j;
          }
          int t = nums[i];
          nums[i] = nums[j];
          nums[j] = t;
        }
        i++;
      }
    }
  }
```
- Python
  
```python
  class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        for i, v in enumerate(nums):
            while v != i:
                if nums[v] == v:
                    return v
                nums[i], nums[v] = nums[v], nums[i]
                v = nums[i]
```
- go
  
```golang
func findRepeatNumber(nums []int) int {
    for i := 0; ; i++ {
        for nums[i] != i {
            j := nums[i]
            if nums[j] == j {
                return j
            }
            nums[i], nums[j] = nums[j], nums[i]
        }
    }
}
```
### 哈希表
- javascript
```javascript
  function findRepeatNumber(nums) {
    const numSet = new Set()
    for(let num of nums) {
      if(numSet.has(num)) {
        return num
      }
      numSet.add(num)
    }
  }
```
- Java
```java
  class Solution {
    public int findRepeatNumber(int[] nums) {
      Set<Integer> numSet = new Hashset<>()
      for(int num: nums) {
        if(!numSet.add(num)) {
          return num
        }
      }
    }
  }
```
- Python
  
```python
  class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
      numSet = set()
      for num in nums:
        if num in numSet:
          return v
        numSet.add(v)
```
- go
  
```golang
func findRepeatNumber(nums []int) int {
  numSet := map[int]bool{}
  for i := 0; ; i++ {
    if numSet[nums[i]] {
      return nums[i]
    }
    numSet[nums[i]] = true
  }
}
```