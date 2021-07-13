[链接](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

题目要求我们判断两个数组是否分别为是压入序列和弹出序列

因此我们可以使用一个辅助栈根据压入序列模拟入栈，然后比较辅助栈顶元素与弹出序列首元素是否相等，如果相等，表明这时候应该将辅助栈顶元素弹出

```javascript
var validateStackSequences = function(pushed, popped) {
  // 辅助栈
  const stack = [];
  // 遍历压入序列，模拟入栈
  for(let i = 0; i < pushed.length; i++) {
    // 入栈
    stack.push(pushed[i]);
    // 判断栈顶元素与弹出序列首元素是否相同，如果相同应该栈出
    while(stack.length && stack[stack.length - 1] === popped[0]) {
      stack.pop();
      popped.shift();
    }
  }
  // 如果辅助栈为空，表明popped为pushed序列的弹出序列
  return stack.length === 0;
}
```