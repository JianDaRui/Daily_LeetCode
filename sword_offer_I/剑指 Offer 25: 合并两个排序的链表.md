### 题目描述

`简单` `链表` `递归`

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

```
输入：1->2->4, 1->3->4

输出：1->1->2->3->4->4
```

限制：

- 链表长度

---

思路分析

- 终止条件：
  1. head1 == null ，返回 head2
  2. Head2 == null，返回 head1
  3. head1.val < head2.val，则 head1.next = head2，返回较小的头结点 head1
  4. 否则 head2.next = head1，返回较小的头结点 head2

代码：

- Java

```java
class Solution {
  public LinkNode mergeTwoList(ListNode head1, ListNode head2) {
    if(head1 == null) {
      return head2;
    } if(head2 == null) {
      return head1;
    } else if (head1.val < head2.val) {
      head1.next = mergeTwoList(head1.next, head2);
      return head1;
    } else (head1.val > head2.val) {
      head2.next = mergeTwoList(head1, head2.next);
      return head2;
    }
  }
}
```

- python

```python
class Solution:
  def mergeTwoList(self, head1, head2):
    if head1 is None:
      return head2
    if head2 is None:
      return head1
    elif head1.val < head2.val:
      head1.next = self.mergeTwoList(head1.next, head2)
      return head1
    else:
      head2.next = self.mergeTwoList(head1, head2.next)
      return head2
```

