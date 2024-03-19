### 题目描述

`简单` `哈希` `数组` `分治` `计数`

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例 1:**

```
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

**限制：**

```
1 <= 数组长度 <= 50000
```

---

思路分析

- [摩尔投票法](https://leetcode.cn/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/solutions/138691/mian-shi-ti-39-shu-zu-zhong-chu-xian-ci-shu-chao-3/)

代码

- Java

```java
class Solution {
    public int inventoryManagement(int[] stock) {
        int x = 0, votes = 0;
        for(int num : stock){
            if(votes == 0) x = num;
            votes += num == x ? 1 : -1;
        }
        return x;
    }
}
 
```

- python

```python
class Solution:
    def inventoryManagement(self, stock: List[int]) -> int:
        votes = 0
        for num in stock:
            if votes == 0: x = num
            votes += 1 if num == x else -1
        return x
```

