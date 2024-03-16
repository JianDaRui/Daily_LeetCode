### 题目描述

`二叉树` `中等` `递归` `单调栈`

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

 

参考以下这颗二叉搜索树：

```
     5
    / \
   2   6
  / \
 1   3
```

**示例 1：**

```
输入: [1,6,3,2,5]
输出: false
```

**示例 2：**

```
输入: [1,3,2,6,5]
输出: true
```

 

**提示：**

1. `数组长度 <= 1000`

---

思路分析

- 后序遍历定义： [ 左子树 | 右子树 | 根节点 ] ，即遍历顺序为 “左、右、根” 。

- 二叉搜索树特点： 左子树中所有节点的值 < 根节点的值；右子树中所有节点的值 > 根节点的值；其左、右子树也分别为二叉搜索树。
- 因此我们可以通过下标划分出数组中的左右子树，通过划分出的左右子树与根节点比较，来判断其是否符合搜索二叉树的定义。
- 为此我们可以从数组的开始和结尾位置依次访问节点通过寻找第一个大于根节点的值的下标 m，则可划分出左子树区间 [i,m−1][i,m-1][*i*,*m*−1] 、右子树区间 [m,j−1][m, j - 1][*m*,*j*−1] 、根节点索引 jj*j* 。

参考：

- [验证二叉搜索树的后序遍历序列](https://leetcode.cn/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/solutions/150225/mian-shi-ti-33-er-cha-sou-suo-shu-de-hou-xu-bian-6/)

代码

- Java

```java
class Solution {
  public boolean verifyTreeOrder(int[] postorder) {
    return recur(postorder, 0, postorder.length - 1);
  }
  boolean recur(int[] postorder, int i, int j) {
    if(i >= j) return true;
    int p = i;
    while(postorder[p] < postorder[j]) {
      p++;
    }
    int m = p
    while(postorder[p] > postorder[j]) {
      p++;
    }
    return p == j && recur(postorder, i, m - 1) && recur(postorder, m, j - 1);
  }
}

```

- python

```python
class Solution:
    def verifyTreeOrder(self, postorder: List[int]) -> bool:
        def recur(i, j):
            if i >= j: return True
            p = i
            while postorder[p] < postorder[j]: p += 1
            m = p
            while postorder[p] > postorder[j]: p += 1
            return p == j and recur(i, m - 1) and recur(m, j - 1)

        return recur(0, len(postorder) - 1)
```

