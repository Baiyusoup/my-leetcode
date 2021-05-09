## 题目

[连接]()

TAG: 

## 解决方案

**暴力法**
设窗口区间为`[i, j]`, 最大值为$x_j$，通过遍历整个窗口获取最大值。

则$x_{j+1}$ = max(nums(i+1), ..., nums(j+1))。

因为数组长度为n，因此共有n-k+1个窗口，遍历一次窗口需要O(k)，因此时间复杂度为O(nk)；

**优化**
如何在每次窗口滑动后，将获取窗口内最大值的时间复杂度从O(k)降为O(1)？


使用单调栈，因为单调栈实现了随意入栈、出栈情况下的O(1)时间获取栈内最小值。

稍为改动一下：使用单调队列，窗口滑动时删除的是列表首部元素。

窗口对象的数据接口为双端队列，本题使用单调队列。每轮遍历时保证单调队列deque：
1. deque内仅包含窗口内元素=> 滑动窗口滑动时，删除元素num(i-1)
2. deque内的元素非严格递减=>每轮窗口滑动添加了元素nums(j+1)，需要将deque内所有 < nums(j+1)的元素删除

流程：
1. 初始化：双端队列deque、结果列表res、数组长度n
2. 滑动窗口：左边界范围i∈[1-k, n-k]，右边界j∈[0, n-1]
   1. 若i > 0且队首元素deque(0) = 被删除元素nums(i-1)时，队首元素出队
   2. 删除deque内所有小于nums(j)的元素，以保持deque递减；
   3. 将nums(j)添加到deque尾部
   4. 若已形成窗口（即i>=0），将窗口最大值（即队首元素deque(0))添加到列表res；


```javascript
const deque = [], res = [],n = nums.length;
// 为形成窗口之前
for(let i = 0; i < k; i++) {
    while(deque.length && deque[deque.length-1] < nums[i]) deque.pop();
    deque.push(nums[i]);
}

res.push(deque[0]);

// 从第二个窗口开始
for(let i = k; i < n; i++) {
  // 如果当前deque首部元素等于nums[i-k]的话，说明首部元素不属于这个窗口，需要删除
  if (deque[0] === nums[i - k]) deque.shift();
  while(deque.length && deque[deque.length - 1] < nums[i]) deque.pop();
  deque.push(nums[i])

  res.push(deque[0]);
}
return res;
```