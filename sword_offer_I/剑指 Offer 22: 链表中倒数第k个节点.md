### 题目描述

`简单` `链表` `快指针`

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

示例：

```
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
```

---

思路分析：

1. 使用快慢指针，都从头结点开始，快指针先走 k 个节点。
2. 这个快慢指针再一起移动，知道快指针走过尾结点时，结束循环。
3. 返回慢指针即可。

代码

- Java

```java
class Solution {
  public ListNode trainingPlan(ListNode head, int k) {
    ListNode faster = head, latter = head;
    while(k != 0) {
      faster = faster.next;
      k--;
    }
    while(faster != null) {
      faster = faster.next;
      latter = latter.next;
    }
    return latter;
  }
}
```

- Python

```python
class Solution:
  def trainingPlan(self, head: ListNode, k: int) -> ListNode:
    fastter, latter = head
    for _ in range(k):
      fastter = fastter.next
    while fastter:
      fastter, latter = fastter.next, latter.next
    return latter
```

