### 题目描述

`简单` `二叉树` `广度优先遍历`

一棵圣诞树记作根节点为 `root` 的二叉树，节点值为该位置装饰彩灯的颜色编号。请按照从左到右的顺序返回每一层彩灯编号，每一层的结果记录于一行。

 

**示例 1：**

![img](https://pic.leetcode.cn/1694758674-XYrUiV-%E5%89%91%E6%8C%87%20Offer%2032%20-%20I_%E7%A4%BA%E4%BE%8B1.png)

```
输入：root = [8,17,21,18,null,null,6]
输出：[[8],[17,21],[18,6]]
```

**提示：**

1. `节点总数 <= 1000`

---

思路分析

- 广度优先遍历

代码

- Java

```java
class Solution {
    public List<List<Integer>> decorateRecord(TreeNode root) {
        Deque<TreeNode> array = new ArrayDeque<>();
        if(root != null) array.addLast(root);

        List<List<Integer>> ans = new ArrayList<>();

        while(!array.isEmpty()) {
            int length = array.size();
            List<Integer> list = new ArrayList<>();
            while(length-- > 0) {
              TreeNode t = array.pollFirst();
                list.add(t.val);
                if (t.left != null) array.addLast(t.left);
                if (t.right != null) array.addLast(t.right);
            }
            ans.add(list);
        }
        return ans;
    }
}
```



- Python

```python
class Solution:
  def decorateRecord(self, root):
    if root is None: return []
    array = collections.deque()
    array.append(root)
    ans = []
    while array:
        list = []
        for _ in range(len(array)):
            node = array.popleft()
            list.append(node.val)
            if node.left: array.append(node.left)
            if node.right: array.append(node.right)
        ans.append(list)
    return ans
```

