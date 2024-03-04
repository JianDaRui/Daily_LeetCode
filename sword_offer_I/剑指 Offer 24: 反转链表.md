题目描述
这是 LeetCode 上的 剑指 Offer 24. 反转链表 ，难度为 简单。

Tag : 「链表」、「迭代」、「递归」

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

示例:

输入: 1->2->3->4->5->NULL

输出: 5->4->3->2->1->NULL
限制：
*0 <= 节点个数 <= 5000*

---

思路1：

- 递归，终止条件 head == null || head.next = null。
- 否则不管链表多长，都将其看做仅有两个节点的链表，就会有如下重复操作：
  - 获取到 head 的下一个节点 head.next， second 。
  - 将 second 的 next 指针指向 head。
  - 将 head 的 next 指针指向 null。
  - 返回 second.
- 递归的话就是每次将第二个节点 head.next 作为新的头指针进行传递：
  - reverseList(head.next)

代码：

- Java

```java
class Solution {
  public ListNode reverseList(ListNode head) {
    if(head == null || head.next == null) return head
    result = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return head
  }
}
```

- Python 

```python
class Solution:
  def reverseList(self, head: ListNode) -> ListNode:
 		if head is None or head.next is None:
      return head
    res = self.reveseList(head.next)
    head.next.next = res
    head.next = None
    return res
    
```



思路二：

- 迭代，将递归栈改为循环



- Java

```java
class Solution {
  public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    while(head !== null) {
      ListNode second = head.next;
      head.next = prev;
      prev.next = head;
      head = second;
    }
    return prev;
  }
}
```

- Python

```python
class Solution:
  def reverseList(self, head: ListNode) -> ListNode:
    prev = None
    while head:
      second = head.next
      head.next = prev
      prev = head
      head = second
    return prev
```

