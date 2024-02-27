### 题目描述

`中等` `回溯` `DFS` `BFS` `动态规划`

地上有一个 m 行 n 列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0] `的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于 k 的格子。例如，当 k 为 18 时，机器人能够进入方格 [35, 37] ，因为 3+5+3+7=18 。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

**示例 1：**

```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2：**

```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示：**

- `1 <= n,m <= 100`
- `0 <= k <= 20`

---

思路分析

- 根据题目可以知道，机器人必须从 [0, 0] 坐标开始移动，所以不必枚举所有方格。
- 每次可以向 4 个方向移动，i + 1、i - 1、j + 1、j + 1。
- 我们使用一个 m * n 的二维矩阵记录访问过的单元格。
- 终止条件 i < 0 || i >= m || j < 0 || j >=0 || fn(x) + fn(y) > k || visited[i] [j] 为 true



代码

- Java

```Java
class Solution {
  int m, n, k, result;
  boolean[][] visited;
  public int movingCount(int m, int n, int k) {
		this.m = m;
    this.n = n;
    this.k = k; 
    this.visited = new boolean[m][n];
 
    dfs(0, 0);
    return result;
  }
  public void dfs(int i , int j) {
    if(i < 0 || i >= m || j < 0 || j >= n || fn(i) + fn(j) > k || visited[i][j]) {
      return;
    }
    // 到达的单元格
    result += 1
    // 标记访问过的
    visited[i][j] = true;
    dfs(i + 1, j);
    //dfs(i - 1, j); 可省略
    dfs(i, j + 1);
    // dfs(i, j - 1);  可省略
  }
  
  public int fn(int num) {
    int s = 0;
    while(num > 0) {
      s += num% 10;
      num /= 10;
    }
    return s;
  }
}
```

- Python

```python
class Solution:
    def __init__(self):
        self.m = 0
        self.n = 0
        self.k = 0
        self.result = 0
        self.visited = []

    def movingCount(self, m, n, k):
        self.m = m
        self.n = n
        self.k = k
        self.visited = [[False for _ in range(n)] for _ in range(m)]
        self.dfs(0, 0)
        return self.result

    def dfs(self, i, j):
        if i < 0 or i >= self.m or j < 0 or j >= self.n or self.fn(i) + self.fn(j) > self.k or self.visited[i][j]:
            return

        self.result += 1

        self.visited[i][j] = True
        self.dfs(i + 1, j)
        self.dfs(i, j + 1)

    def fn(self, num):
        s = 0
        while num > 0:
            s += num % 10
            num //= 10
        return s


```



- javascript

```javascript
/**
 * @param {number} m
 * @param {number} n
 * @param {number} k
 * @return {number}
 */
var movingCount = function(m, n, k) {
    const getSum = (num) => {
        let ans = 0;
        while (num) {
            ans += num % 10;
            num = Math.floor(num / 10)
        }
        return ans;
    }
    let memo = Array.from({ length: m }, () => new Array(n).fill(false));
    let count = 0;
    const dfs = (x, y) => {
        if (x >= m || y >= n || memo[x][y] || getSum(x) + getSum(y) > k) {
            return;
        }
        count++;
        memo[x][y] = true;
        dfs(x + 1, y);
        dfs(x, y + 1)
    }
    dfs(0, 0);
    return count;
};
```



