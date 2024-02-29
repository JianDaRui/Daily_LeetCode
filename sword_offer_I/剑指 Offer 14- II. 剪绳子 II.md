### 题目描述

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m - 1]` 。请问 `k[0]*k[1]*...*k[m - 1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

**示例 1：**

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

**示例 2:**

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

 

**提示：**

- `2 <= n <= 1000`

---

思路分析

- 思路同剪绳子 I
- 使用动态规划求解。
- 如果 n > 1，则可以拆分成至少两段，n 的最大乘积，在所有可以拆分的可能性之间取最大的两段乘积。
  - 比如将 n 拆分成长度 i，n - i。n - i 如果大于 1 , 则又可以至少拆分成两段。
  - 我们使用 dp[n - i] 表示 n - i 长度的绳子所能获取最大乘积。
  - dp[n] = dp[n - i] * i， 0 < i < n。
  - 或这 dp[n] = j * (i - j)。

- 递推公式： dp[n] = max(i * (n - i), dp[n - i] * i, dp[n])

代码：

- Java

```java
class Soultion {
  public int cuttingRope(int n) {
    int[] dp = new int[n + 1];
    for(int i = 2; i < n + 1; i++) {
      for(int j = 1; j < i; j++) {
        dp[i] = Math.max(dp[i], Math.max(j * dp[i - j]), j * (i - j));
      }
    }
    return dp[n];
  }
}
```

- Python

```python
class Solution:
  def cuttingRope(self, n: int) -> int:
    dp = [0] * (n + 1)
    for i in range(2, n + 1):
      for j in range(1, i):
        dp[i] = max(dp[i], j * (i - j), dp[i - j] * j)
        
    return dp[n]
```

