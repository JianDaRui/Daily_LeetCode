### 题目描述

`中等` `链表` `二叉搜索树` `深度优先搜索` `栈` `递归`

将一个 **二叉搜索树** 就地转化为一个 **已排序的双向循环链表** 。

对于双向循环列表，你可以将左右孩子指针作为双向循环链表的前驱和后继指针，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

特别地，我们希望可以 **就地** 完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中最小元素的指针。

**示例 1：**

```
输入：root = [4,2,5,1,3] 

输出：[1,2,3,4,5]

解释：下图显示了转化后的二叉搜索树，实线表示后继关系，虚线表示前驱关系。
```

**示例 2：**

```
输入：root = [2,1,3]
输出：[1,2,3]
```

**示例 3：**

```
输入：root = []
输出：[]
解释：输入是空树，所以输出也是空链表。
```

**示例 4：**

```
输入：root = [1]
输出：[1]
```

 

**提示：**

- `-1000 <= Node.val <= 1000`
- `Node.left.val < Node.val < Node.right.val`
- `Node.val` 的所有值都是独一无二的
- `0 <= Number of Nodes <= 2000`

---

思路分析

- 二叉树中序遍历的演进版。
- 本题的特殊之处在于给定的是一颗二叉搜索树，
  - 二叉搜索树的特点在于 `左节点 < 根节点 < 右节点`
- 本地需要返回一条完成排序（有小到大）的双向链表。
- 这意味着需要进行中序遍历，访问顺序应当是：左节点 < 根节点 < 右节点。
- 以 pre 作为前驱节点，curr 作为当前节点，则应当构建的关系为：
  - pre.right = curr
  - curr.left = pre
- 退栈的时候需要 pre = curr，
- 最后中序遍历结束，需要 head.left = tail，tail.right = head;



代码

- Java

```java
class Solution {
  Node pre, head;
  public Node treeToDoublyList(Node root) {
    if(root == null) return null;
    
    inOrder(root);
    // 遍历结束需要构建 head & tail 的链接
    head.left = pre;
    pre.right = head;
    return head;
  }
  public void inOrder(Node curr) {
    if(curr == null) return;
    inOrder(curr.left);
    if(pre != null) {
      pre.right = curr;
    } else {
      // pre == null, 说明是从左叶子节点开始初始递归
      head = curr;
    }
    curr.left = pre;
    pre = curr;
    // 最终递归结束，pre 为尾结点。
    inOrder(curr.right);
  }
}
```

- python

```python3
class Solution:
  def treeToDoublyList(self, root: 'Node') -> 'Node':
  	self.pre, self.head = None, None
  	def in_order(curr):
  		if curr is None: return
  		in_order(curr.left)
  		
  		if self.pre is None:
  			self.head = curr
  		else:
  			self.pre.right = curr
  		
  		curr.left = self.pre
  		self.pre = curr
  		in_order(curr.right)
  		
   	if root is None: return None
   	
    in_order(root)
  	self.head.left = self.pre
  	self.pre.right = self.head
  	return self.head
```

