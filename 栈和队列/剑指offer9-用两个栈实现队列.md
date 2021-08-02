[链接](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

题目要求我们用两个栈实现一个队列，大概的思路就是用一个栈A负责维护入队顺序，另一个栈B负责维护出队顺序，而且该队列为空的话，需要从A从栈出元素栈入B，这样顺序就不会乱。

```javascript
class CQueue {
  constructor() {
    // 负责元素的入队
    this.tailStack = [];
    // 负责元素的出队
    this.headStack = [];
  }

  // 入队
  appendTail(value) {
    this.tailStack.push(value);
  }

  // 出队
  deleteHead() {
    // 如果出队的栈不为空
    if (this.headStack.length !== 0) {
      return this.headStack.pop();
    } else if (this.tailStack.length !== 0) {
      // 入队的栈不空
      while(this.tailStack.length) {
        this.headStack.push(this.tailStack.pop());
      }
      return this.headStack.pop();
    } else {
      return -1;
    }
  }
}
```