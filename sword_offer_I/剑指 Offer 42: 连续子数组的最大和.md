### 题目描述

`简单` `数组` `分治` `动态规划`

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

 

**示例1:**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

 

**提示：**

- `1 <= arr.length <= 10^5`
- `-100 <= arr[i] <= 100`

---

思路分析

- 要求最优解的题目优先考虑动态规划或者贪心。
- 这里考虑使用动态规划，数组 dp = [] 表示 所有连续天数的最优和。
- *d**p*[*i*] 代表以元素 sales[i]sales[i]*s**a**l**es*[*i*] 为结尾的连续子数组最大和。
- 递推公式 dp[i] = Max(dp[i - 1] + sales[i] , sales[i])

代码

- Java

```java
class Solution {
  public int maxSales(int[] sales) {
    int res = sales[0];
    for(int i = 1; i < sales.length; i++) {
      sales[i] += Math.max(salse[i - 1], 0);
      res = Math.max(res, salse[i]);
    }
    return res;
  }
}
```

- Python

```python
class Solution:
    def maxSales(self, sales: List[int]) -> int:
        for i in range(1, len(sales)):
            sales[i] += max(sales[i - 1], 0)
        return max(sales)
```

