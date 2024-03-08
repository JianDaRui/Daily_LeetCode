### 题目描述

`简单` `二叉树` `递归` `栈`

给定一棵二叉树的根节点 `root`，请左右翻转这棵二叉树，并返回其根节点。

**示例 1：**

![img](https://pic.leetcode.cn/1694686821-qlvjod-%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.png)

```
输入：root = [5,7,9,8,3,2,4]
输出：[5,9,7,4,2,3,8]
```

 

**提示：**

- 树中节点数目范围在 `[0, 100]` 内
- `-100 <= Node.val <= 100`

---

思路分析

- 二叉树后续遍历的演进版本，本质上，大多数二叉树的问题都可以转为前序遍历、中序遍历或者后续遍历。
- 后续遍历的思路是依次访问左节点、右节点、根节点。
- 这里我们优先访问左节点，并将左节点返回作为镜像右节点。
- 同理访问右节点，并返回右节点作为镜像左节点。
- 最后再更改原有树的左右指针引用。

代码

- Java

```java
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
			if(root == null) {
        return root;
      }
      TreeNode right = mirrorTree(root.left);
      TreeNode left = mirrorTree(root.right);
      
      root.left = left;
      root.right = right;
      
      return root;
    }
}
```

- Python

```python
class Solution:
  def mirrorTree(self, root):
    if root is None: return None
    
    left = self.mirrorTree(root.right)
    right = self.mirrorTree(root.left)
    
    root.left = left
    root.right = right
    return root
```



