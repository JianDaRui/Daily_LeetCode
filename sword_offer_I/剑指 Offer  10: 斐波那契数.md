### 题目描述

`简单` `动态规划` `递归`

斐波那契数 （通常用 F(n) 表示）形成的序列称为 斐波那契数列 。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
给定 n ，请计算 F(n) 。

答案需要取模 1e9+7(1000000007) ，如计算初始结果为：1000000008，请返回 1。

示例 1：

输入：n = 2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
示例 2：

输入：n = 3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
示例 3：

输入：n = 4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3

提示：

0 <= n <= 100

---

思路分析:

- 斐波那契数列的定义 f(n + 1) = f(n) + f(n - 1)。
- 第一种思路可以通过递归，递归公式 f(n + 1) = f(n) + f(n - 1)。终止条件 n <= 1。
- 第二种可以通过数组来存储斐波那契数列: array[n + 1] = array[n] + array[n - 1]。
- 第一、二种空间效率比较低，一个使用的是递归栈、一个使用的数组。
- 第三种可以通过降维，通过迭代实现: [a, b] = [b, (a + b)]。

代码：

- Python

```python
class Solution(object):
    def fib(self, n):
        """
        :type n: int
        :rtype: int
        """
        a, b = 0, 1
        for _ in range(n):
          a, b = a, (a + b) % 1000000007
        return a
```

- Java

```java
class Solution {
  public int fib(int n) {
    int a = 0;
    int b = 1;
    for(int i = 0; i < n; i++) {
      int c = (a + b) % 1000000007;
      a = b;
      b = c;
    }
    return a;
  }
}
```

- Javascript

```javascript
const fig = (n) => {
  let a = 0;
  let b = 1;
  for (let i = 0; i < n; i++) {
    [a, b] = [b, (a + b) % 1000000007];
  }
  return a;
};
```
