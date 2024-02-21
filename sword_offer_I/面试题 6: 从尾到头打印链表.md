### 题目描述

`简单` `链表` `递归`

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1：

输入：head = [1,3,2]
输出：[2,3,1]

限制：

0 <= 链表长度 <= 10000

---

### 递归 (推荐)

思路:

- 首先进行 **递** 直到 node === null，这是说明已经访问到链尾。

- 在进行 **归**，归的过程其实就是将节点值放到数组中。

> 递归本质上也是利用的栈。

- Javascript

```javascript
function reversePrint(head) {
  const res = [];
  const dfs = (node) => {
    // 终止条件
    if (node === null) {
      return;
    }
    // 递
    dfs(node.next);
    // 归
    res.push(node.val);
  };
  dfs(head);
  return res;
}
```

- Java

```java
Class Solution {
  ArrayList<Integer> list = new ArrayList<Integer>();

	public int[] reversePrint(LinkNode head) {
		 dfs(head, list);
     int[] ans = new int[list.size()];
     for(int i = 0; i < ans.length; i++) {
       ans[i] = list.get(i);
     }
     return ans;
	}
  public void dfs(ListNode node, ArrayList<Integer> list) {
		if(node == null) {
      return;
    }
    dfs(node.next, list);
    list.add(node.val);
  }
}
```

- Python

```python
class Solution:
    def reverseBookList(self, head: Optional[ListNode]) -> List[int]:
      return self.reverseBookList(head.next) + [head.val] if head else []

```
