### 题目描述

LeetCode: **[剑指 Offer 04. 二维数组中的查找](https://leetcode.cn/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/solution/by-ac_oier-7jo0/)** ，难度为 **中等**。

Tag : 「二叉树搜索树」、「BST」、「二分」、「查找」

在一个 $n \times m$ 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:
```
现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

给定 target = 5，返回 true。
给定 target = 20，返回 false。
```

限制：
* $0 <= n <= 1000$
* $0 <= m <= 1000$

---
### 二分法

```javascript
  function findTargetNumber (plants, target) {
    let i = plants.length - 1;
    let j = 0;
    while(i >= 0 && j < plants[0].length) {
      const item = plants[i][j]
      if(item > target) {
        i -= 1
      } else if (item < target) {
        j += 1
      } else {
        return true
      }
    }
    return false
  }
```

```python
  class Solution:
    def findTargetNumber(self, plants: List[List[int]], target: int) -> bool:
      i, j = len(plants) - 1, 0
      while i >= 0 and j < len(plants[0]):
        if plants[i][j] > target: i -= 1
        elif plants[i][j] < target: j += 1
        else: return True
      return False
```

```java
  class Solution {
    public boolean findTargetNumber(int[][] plants, int target) {
      int i = plants.length - 1;
      int j = 0;

      while(i >= 0 && j < plants[0].length - 1) {
        int item = plants[i][j];
        if(item > target) {
          i -= 1;
        } else if(item < target) {
          j += 1;
        } else {
          return true;
        }
      }
      return false;
    }
  }
```

```golang
func findTargetNumber(plants [][]int, target int) bool {
  i, j = len(plants) - 1, 0;
  for i >= 0 && j < len(plants[0]) {
    item = plants[i][j]
    if item > target {
      i -= 1
    } else if item < target {
      j += 1
    } else {
      return true
    }
  }
  return false
}
```