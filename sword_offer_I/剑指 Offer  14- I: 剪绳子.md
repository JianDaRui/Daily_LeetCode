### 题目描述

`中等` `动态规划`

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n 都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m-1]` 。请问 `k[0]*k[1]*...*k[m-1]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为 2、3、3 的三段，此时得到的最大乘积是18。

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

- `2 <= n <= 58`

---

思路分析

- 求最大、最优解一般优先考虑**贪心**或者**动态规划**。
- 这题中首先尝试动态规划进行解答，我们使用 dp[n]，表示长度为 n 时，可以获取的最大乘积。
- 当 n <= 3 时，不需要拆分就可以获取最大值，因此 dp[1] = 1, dp[2] = 2, dp[3] = 3。
  - n > 3 时，可以拆分为：i , n - i 
    - i  的取值范围为  1 <= i < n。表示我们
    - 如果 n - i > 3 ，则 n - i 可以继续进行拆分，这时 dp[n] = i * dp[n - i]，需要。
    - 如果不再拆分，则 dp[n] = i * (n - i)。
    - 或者 n 直接不拆分，则为 n。
  - dp[n] 每次要取最优解，因此 `dp[n] = max(n, i * dp[n - i], i * (n - i ))`

代码：

- Java

```java
class Solution {
	public int cuttingRope(int n) {
		int[] dp = new int[n + 1];
    dp[1] = 1;
    for(int i = 2; i < n + 1; i++) {
      for(int j = 1; j < i; j++) {
        dp[i] = Math.max(Math.max(dp[i], dp[i - j] * j), (i - j) * j);
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
    dp = [1] * (n + 1)
    for i in range(2, n + 1):
      for j in range(1, i):
        dp[i] = max(dp[i], dp[i - j] * j, (i - j) * j)
    
    return dp[n]

```

