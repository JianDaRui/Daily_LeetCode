### 题目描述

`中等` `矩阵` `模拟`

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

 

**示例 1：**

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

**示例 2：**

```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

 

**限制：**

- `0 <= matrix.length <= 100`
- `0 <= matrix[i].length <= 100`

---

思路分析

- 从外层向内层逐层遍历打印
- 分别定义左右边界 left、right，上下边界 top、bottom。
- left++、right-- 逐层向内收缩
- Top--、bottom++ 逐层向中间搜索。

代码

- Java

```java
class Solution {
  public int[] spiralOrder(int[][] matrix) {
    if(matrix.length == 0 || matrix[0].length == 0) {
      return new int[] {};
    }
    int row = matrix.length;
    int column = matrix[0].length;
    int top = 0, bottom = row - 1, left = 0, right = column - 1;
    int[] res = new int[row * column];
    int i = 0;
    while(left <= right && top <= bottom) {
      // 从左到右
      for(int j = left; j <= right; j++) {
        ans[i++] = matrix[left][j];
      }
      // 从上到下
      for(int j = top; j <= bottom; j++) {
        ans[i++] = matrix[j][right];
      }
      if(left < right && top < bottom) {
        // 从右到左
        for(int j = right; j >= left; j--) {
          ans[i++] = matrix[bottom][j];
        }
        // 从下到上
        for(int j = bottom; j >= top; j--) {
          ans[i++] = matrix[j][left];
        }
      }
      left++;
      right--;
      bottom--;
      top++; 
    }
    return ans
  }
}
```

- Python3

```python3
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix or not matrix[0]:
            return []
        m, n = len(matrix), len(matrix[0])
        ans = []
        top, bottom, left, right = 0, m - 1, 0, n - 1
        while left <= right and top <= bottom:
            ans.extend([matrix[top][j] for j in range(left, right + 1)])
            ans.extend([matrix[i][right] for i in range(top + 1, bottom + 1)])
            if left < right and top < bottom:
                ans.extend([matrix[bottom][j] for j in range(right - 1, left - 1, -1)])
                ans.extend([matrix[i][left] for i in range(bottom - 1, top, -1)])
            top, bottom, left, right = top + 1, bottom - 1, left + 1, right - 1
        return ans
```

