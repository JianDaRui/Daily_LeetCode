### 题目描述

`中等` `二叉树` `先序遍历` `递归`

给定两棵二叉树 tree1 和 tree2，判断 tree2 是否以 tree1 的某个节点为根的子树具有 相同的结构和节点值 。
注意，空树 不会是以 tree1 的某个节点为根的子树具有 相同的结构和节点值 。

示例 1：

输入：tree1 = [1,7,5], tree2 = [6,1]
输出：false
解释：tree2 与 tree1 的一个子树没有相同的结构和节点值。

示例 2：

输入：tree1 = [3,6,7,1,8], tree2 = [6,1]
输出：true
解释：tree2 与 tree1 的一个子树拥有相同的结构和节点值。即 6 - > 1。

提示：

0 <= 节点个数 <= 10000

---

思路分析

- 二叉树先序遍历的演进版，
- 先遍历 A 的每个节点，将 A 的每个节点后的二叉树看做一个独立的二叉树，将其与 B 比较
- 在通过先序遍历比较 A 当前节点与 B，比较的结束条件 B == null || A == null || A.val != B.val 的情况下，返回 false。
- 否则递归比较两者的左子树和右子树

代码

- Java

```java
class Solution {
  public boolean isSubStructure(TreeNode A, TreeNode B) {
    if(A != null && B != null) {
      return isCommonTree(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }
    
    return false;
  }
  public boolean isCommonTree(TreeNode A, TreeNode B) {
    if(B == null) {
      return true;
    }
    if(A == null || A.val != B.val) return false;
    return isCommonTree(A.left, B.left) && isCommonTree(A.right, B.right);
  }
}

```

- Python

```python
class Solution:
  def isSubSructure(self, A, B):
    def isCommon(A, B):
      if not B: return True
      if not A or A.val != B.val: return False
      return isCommon(A.left, B.left) and isCommon(A.right, B.right)
    return bool(A and B) and (isCommon(A, B) or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B))
```
