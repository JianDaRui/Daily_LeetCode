### 题目描述

`简单` `数组` `堆` `分治` `排序`

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

**示例 1：**

```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

**示例 2：**

```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

 

**限制：**

- `0 <= k <= arr.length <= 10000`
- `0 <= arr[i] <= 10000`

---

- 像这种求数组中最小/最大的 k 个数的题目优先考虑小顶堆/大顶堆。
- 如果是采取排序的解法可以考虑使用快排或者归并排序



- Java

```java
class Solution {
  public int[] getLeastNumbers (int[] arr, int k) {
    int res = new int[k];
    if(k == 0) {
      return res;
    }
    
    PriorityQueue<Integer> queue = new PriorityQueue<Integer>(new Comparator<Integer>() {
      public int compare(Integer num1, Integer num2) {
        return num2 - num1;
      }
    });
    
    for(int i = 0; i < k; i++) {
      queue.offer(arr[i]);
    }
    for(int i = k; i < arr.length; i++) {
      if(queue.peek() > arr[i]) {
        queue.poll();
        queue.offer(arr[i]);
      }
    }
    
    for(int i = 0; i < k; i++) {
      res[i] = queue.poll();
    }
    return res;
  }
}
```

- Python

```python3
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        if k == 0:
            return list()

        hp = [-x for x in arr[:cnt]]
        heapq.heapify(hp)
        for i in range(k, len(arr)):
            if -hp[0] > arr[i]:
                heapq.heappop(hp)
                heapq.heappush(hp, -arr[i])
        ans = [-x for x in hp]
        return ans
```

