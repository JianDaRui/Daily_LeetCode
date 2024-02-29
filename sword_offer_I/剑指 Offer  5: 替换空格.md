### 题目描述

`简单` `字符串`

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

**限制：**

```
0 <= s 的长度 <= 10000
```

---

### 内置方法替换

- Javascript

```javascript
var replaceSpace = function (s) {
    return s.split(' ').join('%20');
};
```

- Java

```java
Class Solution {
	public String replaceString(String s) {
		return s.replaceAll(" ", "%20");
	}
}
```

- Python

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        return s.replace(' ', '%20')\
```

- Go

```go
func replaceSpace(s string) string {
    return strings.Replace(s, " ", "%20", -1)
}
```

### 遍历替换

- javascript

```javascript
var replaceSpace = function (s) {
		const res = []
		for(let i of s) {
		 	if(i === " ") {
				res.push("%20")
			} else {
				res.push(i)
			}
		}
    return res.join('');
};
```

- Java

```Java
class Solution {
  public String replaceSpace(String s) {
    StringBuilder res = new StringBuilder();
    for(Character c : s.toCharArray()) {
      if(c == " ") {
        res.push("%20")
      } else {
        res.append(c);
      }
    }
    return res.toString();
  }
}
```

- Python

```python
class Solution:
    def pathEncryption(self, path: str) -> str:
        res = []
        for c in path:
            if c == '.': res.append(' ')
            else: res.append(c)
        return "".join(res)
```

