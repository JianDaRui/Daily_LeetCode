## 题目描述

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

**示例 1：**

```
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```

**示例 2：**

```
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```

 

**限制：**

- 最多会对 `addNum、findMedian` 进行 `50000` 次调用。

---

思路分析



代码

- Java

```java
class MedianFinder {
    private PriorityQueue<Integer> q1 = new PriorityQueue<>();
    private PriorityQueue<Integer> q2 = new PriorityQueue<>((a, b) -> b - a);

    /** initialize your data structure here. */
    public MedianFinder() {
    }

    public void addNum(int num) {
        if (q1.size() > q2.size()) {
            q1.offer(num);
            q2.offer(q1.poll());
        } else {
            q2.offer(num);
            q1.offer(q2.poll());
        }
    }

    public double findMedian() {
        if (q1.size() > q2.size()) {
            return q1.peek();
        }
        return (q1.peek() + q2.peek()) / 2.0;
    }
}
```

- python

```python3
class MedianFinder:
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.q1 = []
        self.q2 = []

    def addNum(self, num: int) -> None:
        if len(self.q1) > len(self.q2):
            heappush(self.q2, -heappushpop(self.q1, num))
        else:
            heappush(self.q1, -heappushpop(self.q2, -num))

    def findMedian(self) -> float:
        if len(self.q1) > len(self.q2):
            return self.q1[0]
        return (self.q1[0] - self.q2[0]) / 2
 
```