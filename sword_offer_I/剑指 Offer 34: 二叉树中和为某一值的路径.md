### 题目描述

`中等` `二叉树` `递归` `回溯`

给你二叉树的根节点 `root` 和一个整数目标和 `targetSum` ，找出所有 **从根节点到叶子节点** 路径总和等于给定目标和的路径。

**叶子节点** 是指没有子节点的节点。



**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

**示例 3：**

```
输入：root = [1,2], targetSum = 0
输出：[]
```

 

**提示：**

- 树中节点总数在范围 `[0, 5000]` 内
- `-1000 <= Node.val <= 1000`
- `-1000 <= targetSum <= 1000`

---

思路分析：

- 二叉树前序遍历的演进版，需要在退栈的过程中去进行回溯操作。
- 当 root == null 的时候，直接结束递归。
- 使用 path 去存储访问的路径。
- 在前序遍历依次访问各个节点的时候，每次将 target 减去当前节点的值作为新的 target，当 target == 0 && root.left == null && root.right == null 的时候，则找到一条符合条件路径。
- 在退栈的过程中，如果没有找到合适的，则需要将 path 的最后一个值弹出（也就是当前节点的值）

代码：

- Java

```java
class Solution {
  LinkedList<List<Integer>> result = new LinkedList<>();
  LinkedList<Integer> path = new LinkedList<>();
  public List<List<Integer>> pathTarget(TreeNode root, int target) {
		preOrder(root, target);
    return result;
  }
  public void preOrder(TreeNode root, int target) {
    if(root == null) {
      return;
    }
    
    target -= root.val;
    path.add(root.val);
    if(root.left == null && root.right == null && target == 0) {
      result.add(new LinkedList(path));
    }
    preOrder(root.left, target);
    preOrder(root.right, target);
    path.removeLast();
  }
}
```

- python

```python
class Solution:
  def pathTarget(self, root, target):
    result, path = [], []
    def preOrder(root, target):
      if not root: return
      target -= root.val
      path.append(root.val)
      if target == 0 and not root.left and not root.right:
        result.append(list(path))
      preOrder(root.left, target)
      preOrder(root.right, target)
      path.pop()
    preOrder(root, target)
    return result
```

