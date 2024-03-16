### 题目描述

`中等` `二叉树` `广度优先搜索`

一棵圣诞树记作根节点为 `root` 的二叉树，节点值为该位置装饰彩灯的颜色编号。请按照从 **左** 到 **右** 的顺序返回每一层彩灯编号。

 

**示例 1：**

![img](https://pic.leetcode.cn/1694758674-XYrUiV-%E5%89%91%E6%8C%87%20Offer%2032%20-%20I_%E7%A4%BA%E4%BE%8B1.png)

```
输入：root = [8,17,21,18,null,null,6]
输出：[8,17,21,18,6]
```

 

**提示：**

1. `节点总数 <= 1000`

---

思路分析

- 根据题意，可以使用广度优先遍历。
- 将每一层的节点按顺序存在一个队列中。
- 在对队列进行遍历取出节点的值即可。

代码

- java

```java
class Solution {
    public int[] decorateRecord(TreeNode root) {
			if(root == null) return new int[0];
      Queue<TreeNode> queue = new LinkedList<>(){{ add(root) }};
      ArrayList<Integet> ans = new ArrayList<>();
      while(!queue.isEmpty()) {
        TreeNode node = queue.poll();
        ans.add(node.val);
        if(node.left != null) queue.add(node.left);
        if(node.right != null) queue.add(node.right);
      }
      
      int[] res = new int[ans.size()];
      for(int )
    }
}
```

- python

```python3
class Solution:
    def decorateRecord(self, root: TreeNode) -> List[int]:
        if not root: return []
        res, queue = [], collections.deque()
        queue.append(root)
        while queue:
            node = queue.popleft()
            res.append(node.val)
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)
        return res
```



