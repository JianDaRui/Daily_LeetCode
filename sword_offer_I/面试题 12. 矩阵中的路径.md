### 题目描述

`中等` `矩阵` `回溯` `DFS`

给定一个 `m x n` 二维字符网格 `board` 和一个字符串单词 `word` 。如果 `word` 存在于网格中，返回 `true` ；否则，返回 `false` 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
输出：true
```

**示例 3：**

![img](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
输出：false
```

**提示：**

- `m == board.length`
- `n = board[i].length`
- `1 <= m, n <= 6`
- `1 <= word.length <= 15`
- `board` 和 `word` 仅由大小写英文字母组成

---

思路分析

- 典型的 DFS 问题。
- 单词的开头位置可能是网格中的任何一个位置，所以需要遍历网格中的所有单元格，从每一个单元格开始进行 dfs，直到匹配。
- dfs 需要从每个单元格的 4 个方向出发进行递归，分别是： i + 1, i - 1, j + 1, j - 1。
- DFS 终止条件 i 或者 j 越界，或者 board[i] [j] 不等于 word[k] 。每次匹配到需要对已经遍历的网格进行标记。
- 回溯过程中，再将 board[i] [j] 还原，便于下一次 DFS。

代码

- Java

```Java
Class Solution {
  public boolean exist(char[][] board, String word) {
      char[] words = word.toCharArray();
      for(int i = 0; i < board.length; i++) {
          for(int j = 0; j < board[0].length; j++) {
              if (dfs(board, words, i, j, 0)) return true;
          }
      }
      return false;
    }

  public boolean dfs(char[][] board, String word, int i, int j, int k) {
    if(i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word[k]) {
      return false
    }

    board[i][j] = '.';
    boolean res = dfs(board, word, i + 1, j, k + 1) || dfs(board, word, i - 1, j, k + 1) ||
                  dfs(board, word, i, j + 1, k + 1) || dfs(board, word, i , j - 1, k + 1);
    board[i][j] = word[k];
    return res
  }
}

```

- Python

```Python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        m, n = len(board), len(board[0])

        def dfs(i, j, k):
          if i < 0 or j < 0 or i >= m or j >= n or board[i][j] != word[k]: return False
          if k == len(word) - 1: return False

          board[i][j] = '.'

          res = dfs(i + 1, j, k + 1) or dfs(i - 1, j, k + 1) or dfs(i, j + 1, k + 1) or dfs(i, j - 1, k + 1)

          board[i][j] = word[k]

          return res
        for i in range(m):
          for j in range(n):
            if dfs(i, j, 0): return True

        return False
```

- Javascript

```Javascript
var exist = function(board, word) {
    const m = board.length
    const n = board[0].length

    const dfs = function(i, j, k) {
        if (i < 0 || j < 0 || i >= m || j >= n || board[i][j] !== word[k]) {
            return false
        }
        if(k === word.length - 1) return true
        board[i][j] = '.'
        const res = dfs(i + 1, j, k + 1) || dfs(i - 1, j, k + 1)
                    ||dfs(i, j + 1, k + 1) || dfs(i, j - 1, k + 1)
        board[i][j] = word[k]
        return res
    }

    for(let i = 0; i < m; i++) {
        for(let j = 0; j < n; j++) {
            if(dfs(i, j, 0)) {
                return true
            }
        }
    }
    return false
};
```
