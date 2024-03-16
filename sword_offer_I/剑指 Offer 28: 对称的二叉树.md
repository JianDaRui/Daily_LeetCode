### 题目描述

`简单` `二叉树` `递归` `栈`

请设计一个函数判断一棵二叉树是否 **轴对称** 。

 

**示例 1：**

![img](https://pic.leetcode.cn/1694689008-JaaRdV-%E8%BD%B4%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%911.png)

```
输入：root = [6,7,7,8,9,9,8]
输出：true
解释：从图中可看出树是轴对称的。
```

**示例 2：**

![img](https://pic.leetcode.cn/1694689054-vENzHe-%E8%BD%B4%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%912.png)

```
输入：root = [1,2,2,null,3,null,3]
输出：false
解释：从图中可看出最后一层的节点不对称。
```

 

**提示：**

```
0 <= 节点个数 <= 1000
```

---

思路分析

- 先序遍历的演进版本
- 这次递归访问根节点的时候，需要传两个树节点。
- 依次判断 left.val == right.val && left.right.val == right.left.val && left.left.val == light.right.val。
- 终止条件 left == null && right == null 返回 true。
- 如果 left == null || right == null 则返回 false

代码

- Java

```java
class Solution {
  	public boolean checkSymmetricTree(TreeNode root) {
				if(root == null) {
          return true;
        }
      	
      	return checkTree(root, root);
    }
  	public boolean checkTree(TreeNode left, TreeNode right) {
		if(left == null && right != null) {
          return false;
        }
      	if(left != null && right == null) {
          return false;
        }
        if(left == null && right == null) {
          return true;
        }
      	return left.val == right.val && checkTree(left.right, right.left) && checkTree(left.left, right.right);
    }
}
```

- python

```python
class Solution:
  def checkSymmetricTree(root):
    def checkTree(left, right):
      if(left is None and right is None): return True
      if(left is None or right is None): return False
      return left.val == right.val and checkTree(left.left, right.right) and checkTree(left.right, right.left)
    return checkTree(root, root)
```

