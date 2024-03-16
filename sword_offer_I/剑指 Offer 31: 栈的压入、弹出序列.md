### 题目描述

`中等` `栈`

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

 

**示例 1：**

```
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

**示例 2：**

```
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

 

**提示：**

1. `0 <= pushed.length == popped.length <= 1000`
2. `0 <= pushed[i], popped[i] < 1000`
3. `pushed` 是 `popped` 的排列。

---

思路分析

- 遍历 `pushed` 序列，将每个数 `v` 依次压入栈中。
- 压入后检查栈顶是不是 `popped` 序列中下一个要弹出的值。
- 如果是就循环把栈顶元素弹出。

- 遍历结束，如果 `popped` 序列已经到末尾或者 stack 为空，说明是一个合法的序列，否则不是。

代码

- Java

```java
class Solution {
  public boolean validateStackSequences(int pushed, int popped) {
        Stack<Integer> stack = new Stack<>();
        int j = 0;
        for(int v : pushed) {
            stack.push(v);
            while(!stack.isEmpty() && stack.peek() == popped[j]) {
                stack.pop();
                j++;
            }
        }
        return stack.isEmpty();
    }
}
```

- python

```python
class Solution:
    def validateBookSequences(self, pushed: List[int], popped: List[int]) -> bool:
        stack, i = [], 0
        for num in pushed:
            stack.append(num) # num 入栈
            while stack and stack[-1] == popped[i]: # 循环判断与出栈
                stack.pop()
                i += 1
        return not stack

```

