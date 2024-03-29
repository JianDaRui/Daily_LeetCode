### 题目描述

`中等` `二叉树` `递归` `数组` `哈希表`

给定两个整数数组 `preorder` 和 `inorder` ，其中 `preorder` 是二叉树的**先序遍历**， `inorder` 是同一棵树的**中序遍历**，请构造二叉树并返回其根节点。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出: [3,9,20,null,null,15,7]
```

**示例 2:**

```
输入: preorder = [-1], inorder = [-1]
输出: [-1]
```

 

**提示:**

- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` 和 `inorder` 均 **无重复** 元素
- `inorder` 均出现在 `preorder`
- `preorder` **保证** 为二叉树的前序遍历序列
- `inorder` **保证** 为二叉树的中序遍历序列

---

### 递归重建

思路分析：

- 本题可以看做是 **前序遍历** 的进阶版。
- 前序遍历返回的结构：根节点 【左子树】【右子树】，中序遍历返回的结构：【左子树】根节点【右子树】
- 每次可以根据前序遍历找到根节点 `value`。
- 并根据根节点 `value` 在中序遍历的位置 `index`
- 这时可以根据 `index` 划分出 **左子树的前序 & 中序遍历序列**，**右子树的前序 & 中序遍历序列**。
- 以此思路递归构建出二叉树。

题解

- JavaScript

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function(preorder, inorder) {
    const createTree = (preorder, inorder) => {
        if(preorder.length === 0) {
            return null;
        }
      	// 获取根节点 val
        const val = preorder[0];
      	// 获取根节点在中序遍历的位置 index
        const index = inorder.indexOf(val);
        // 左子树的中序遍历
      	const leftTreeInorder = inorder.slice(0, index)
        // 右子树的中序遍历
      	const rightTreeInorder = inorder.slice(index + 1)
        // 左子树的前序遍历
      	const leftTreePreorder = preorder.slice(1, index + 1)
        // 右子树的前序遍历
      	const rightTreePreorder = preorder.slice(index + 1)
        
        let root = new TreeNode(val);
        root.left = createTree(leftTreePreorder, leftTreeInorder)
        root.right = createTree(rightTreePreorder, rightTreeInorder)
        return root;
    }
    
    return createTree(preorder, inorder)
};
```

- Java

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder.length == 0) {
            return null;
        }
      	// 获取根节点 val
        int val = preorder[0];
      	// 获取根节点在中序遍历的位置 index
        int index = findIndex(inorder, index);
        int[] leftTreeInorder = Arrays.copyOfRange(inorder, 0, index);
        int[] rightTreeInorder = Arrays.copyOfRange(inorder, index + 1, inorder.length);
        int[] leftTreePreorder = Arrays.copyOfRange(preorder, 1, index + 1);
        int[] rightTreePreorder = Arrays.copyOfRange(preorder, index + 1, preorder.length);
        
        TreeNode root = new TreeNode(val);
        root.left = buildTree(leftTreePreorder, leftTreeInorder);
        root.right = buildTree(rightTreePreorder, rightTreeInorder);
        return root;
    }
  	private int findIndex(int[] array, int val) {
      for(int i = 0; i < array.length; i++) {
        if(array[i] == val) {
          return i
        }
      }
      return -1;
    }
}

```

- Python

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if not preorder:
            return None
        # 获取根节点 val
        val = preorder[0]
        # 获取根节点在中序遍历的位置 index
        index = inorder.index(val)
        # 左子树的中序遍历
        left_tree_inorder = inorder[:index]
        # 右子树的中序遍历
        right_tree_inorder = inorder[index + 1:]
        # 左子树的前序遍历
        left_tree_preorder = preorder[1:index + 1]
        # 右子树的前序遍历
        right_tree_preorder = preorder[index + 1:]
        root = TreeNode(val)
        root.left = self.buildTree(left_tree_preorder, left_tree_inorder)
        root.right = self.buildTree(right_tree_preorder, right_tree_inorder)
        return root;
        
      
```
