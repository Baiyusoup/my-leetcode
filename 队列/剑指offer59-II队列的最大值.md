[链接](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

看到题目要求的用一个队列来实现找到最大值的时间复杂度为O(1)，让我不经想起了以前做过的[类似题](剑指offer59-I滑动窗口的最大值.md)，第一想到的就是单调队列来实现。

通过构建一个递减列表来保存队列所有递减的元素，递减队列随着入队和出队操作实时更新，这样队列最大的元素始终对应递减列表的首元素，实现了获取最大值的O(1)时间复杂度。

为了实现这个递减列表，需要使用双向队列
1. 当执行入队操作时，若入队一个比队列某些元素更大的数字x，则为了保持此列表递减，需要将双向队列尾部所有小于x的元素弹出。
2. 当执行出队操作时，若出队的元素是最大，则双向队列需要同时将首元素出队，以保持队列和双向队列的元素一执行。



我做这题的时候，审错题了，以为pop_front()返回的元素也是最大值。

```javascript
var MaxQueue = function() {
  // 普通队列，保存入队序列
  this.queue = [];

  // 单调队列，保证首元素为队列中的最大值，即满足题目要求的O(1)复杂度
  this.dequeue = [];
};

/**
 * @return {number}
 */
MaxQueue.prototype.max_value = function() {
    // 如果队列为空的话，返回-1，否则返回队列中的最大元素
    return this.queue.length === 0 ? -1 : this.dequeue[0];
}; 

/** 
 * @param {number} value
 * @return {void}
 */
MaxQueue.prototype.push_back = function(value) {
    // 入队
    this.queue.push(value);

    // 维护单调队列
    while(this.dequeue.length && this.dequeue[this.dequeue.length - 1] < value) {
      // 将单调队列中小于value的元素都删掉，保证单调性
      this.dequeue.pop();
    }
    this.dequeue.push(value);
};

/**
 * @return {number}
 */
MaxQueue.prototype.pop_front = function() {
    // 如果队列为空，返回-1
    if (!this.queue.length) return -1;
    // 如果出队元素和单调队列的首元素一样，那么单调队列要将首元素出队，保持一执性
    const value = this.queue.shift();
    if (value === this.dequeue[0]) {
      this.dequeue.shift();
    }
    return value;
};
```