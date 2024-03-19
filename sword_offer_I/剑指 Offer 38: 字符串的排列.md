### 题目描述

`中等` `字符串` `回溯` `递归`

输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

**示例:**

```
输入：goods = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

**限制：**

```
1 <= s 的长度 <= 8
```

---

思路分析

- 经典递归回溯题。
- 终止条件字母组合 path.length == s.length。
- 需要递归的层数为 path.length。
- 每次进入下一层的使用使用 map 标记使用过的字母 ，map[i] = true
- 当退栈的时候再将 map[i] = false。
- 使用 set 进行去重。

代码

- Javascript

```javascript
/**
 * @param {string} s
 * @return {string[]}
 */
var goodsOrder = function (s) {
    let res = new Set();
    let map = {};
    let dfs = (path) => {
        if (path.length === s.length) {
            res.add(path);
            return
        }
        for (let i = 0; i < s.length; i++) {
            if (map[i]) continue;
            map[i] = true;
            dfs(path + s[i]);
            map[i] = false;
        }
    }
    dfs('');
    return [...res];
};
```

- Java

```java
class Solution {
  List<String> res = new LinkedList<>();
  char[] arr
  public String[] goodsOrder(String goods) {
    arr = goods.toCharArray();
    dfs(0);
    return res.toArray(new String[res.size()]);
  }
  void dfs(int x) {
    if(x == arr.length - 1) {
      res.add(String.valueOf(arr));
      return;
    }
    HashSet<Character> set = new HashSet<>();
    for(int i = x; i < arr.length; i++) {
      if(set.contains(arr[i])) continue;
      set.add(arr[i]);
      swap(i, x);                   
      dfs(x + 1);                      
      swap(i, x);
    }
  }
  void swap(int a, int b) {
      char tmp = arr[a];
      arr[a] = arr[b];
      arr[b] = tmp;
  }
}
```

- python

```python
class Solution:
  def goodsOrder(self, goods: str) -> List[str]:
    arr, res = list(goods), []
    
    def dfs(x):
      if x == len(arr) - 1:
        res.append('', join(arr))
        return
      hmap = set()
      for i in range(x, len(arr)):
        if arr[i] in hmap: continue
        hmap.add(arr[i])
        arr[i], arr[x] = arr[x], arr[i] 
        dfs(x + 1)      
        arr[i], arr[x] = arr[x], arr[i] 
        
    dfs(0)
    return res

```



