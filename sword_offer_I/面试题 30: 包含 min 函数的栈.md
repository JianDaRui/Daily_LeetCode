### 题目描述

`简单` `栈`

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

**示例:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

 

**提示：**

1. 各函数的调用总次数不超过 20000 次

---

思路分析

- 通常获取栈结构中最小值的方法是进行遍历，时间复杂度为 O(n)。
- 这里使用一个栈进行操作，并不现实。
- 所以使用辅助栈来存储一份 主栈中的降序元素子序列。
- 比如主栈序列是：9  10 7 3 5，则辅助栈是 9 7 3。
- 

代码

- Java

```java
class Solution {
  Stack<Integet> A, B;
  public MinStack() {
    A = new Stack<>();
    B = new Stack<>();      
  }
  public void push (int x) {
    A.add(x);
    if(B.empty() || B.peek() >= x) {
      B.add(x);
    }
  }
  public void pop() {
    if(A.pop().equals(B.peek())) {
      B.pop();
    }
  }
  public int top() {
    return A.peek();
  }
  public int getMin() {
    return B.peek();
  }
}
```

- Python

```python
class MinStack:
  def __int__(self):
    self.A, self.B = [], []
  def push(self, x):
    self.A.append(x)
    if not self.B or self.B[-1] >= x:
      self.B.append(x)
  def pop(self):
    if self.A.pop() == self.B[-1]:
      self.B.pop()
  def top(self):
    return self.A[-1]
  def getMin(self):
    return self.B[-1]
```

