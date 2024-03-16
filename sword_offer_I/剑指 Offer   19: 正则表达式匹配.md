### 题目描述

`困难` `动态规划` `字符串`

请实现一个函数用来匹配包含`'. '`和`'*'`的正则表达式。模式中的字符`'.'`表示任意一个字符，而`'*'`表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串`"aaa"`与模式`"a.a"`和`"ab*ac*a"`匹配，但与`"aa.a"`和`"ab*a"`均不匹配。

**示例 1:**

```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```

**示例 2:**

```
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```

**示例 3:**

```
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```

**示例 4:**

```
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```

**示例 5:**

```
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```

- `s` 可能为空，且只包含从 `a-z` 的小写字母。
- `p` 可能为空，且只包含从 `a-z` 的小写字母以及字符 `.` 和 `*`，无连续的 `'*'`。

---

思路分析

参考：[逐行详细讲解，由浅入深，dp和递归两种思路](https://leetcode.cn/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solutions/92888/zhu-xing-xiang-xi-jiang-jie-you-qian-ru-shen-by-je/)

代码

- Java

```java
class Solution {
  public boolean isMatch(String A, String B) {
    int n = A.length();
    int m = B.length();
    boolean[] f = new boolean[n + 1][m + 1];
    
    for(int i = 0; i <= n; i++) {
      for(int j = 0; j <= m; j++){
        if(j == 0) {
          f[i][j] = i == 0;
        } else {
          if(B.charAt(j - 1) != '*') {
            if(i > 0 && (A.charAt(i - 1) == B.charAt(j - 1) || B.charAt(j - 1) == '.')) {
              f[i][j] = f[i - 1][j - 1];
            }
          } else {
            if(j >= 2) {
              f[i][j] |= f[i][j - 2];
            }
            if(i >= 1 && j >= 2 && (A.charAt(i - 1) == B.charAt(j - 2) || B.charAt(j - 2) == '.')) {
              f[i][j] |= f[i - 1][j];
            }
          }
        }
      }
    }
    return f[n][m];
  }
}
```

- Python

```python
class Solution:
  def isMatch(self, A, B):
    n = len(A)
    m = len(B)
    f = [[False] * (m + 1) for _ in range(n + 1)]
    for i in range(n + 1):
      for j in range(m + 1):
        if j == 0:
          f[i][j] = i == 0
        else:
          if B[j - 1] != '*':
            if i > 0 and (A[i - 1] == B[j - 1] or B[j - 1] == '.'):
              f[i][j] = f[i - 1][j - 1]
          else：
          	if j >= 2:
              f[i][j] |= f[i][j - 2]
            if i >= 1 and j >= 2 and (A[i - 1] == B[j - 2] or B[j - 2] == '.'):
              f[i][j] |= f[i - 1][j]
            
          
   return f[n][m]
```

