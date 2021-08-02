## 题目
从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

[连接](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

TAG: EASY

## 解题方案
既然题目要求的是按层打印，第一想到的肯定是广度优先遍历了，那么问题又来了。

我怎么知道队列里面的元素哪部分是同一层的呢？

我们可以通过计数啊，当我们循环次数达到一定时就表明本层的节点遍历完成了，而这个循环次数我们可以用队列的长度。

```javascript
var levelOrder = function(root) {
    if(!root) return [];
    const queue = [root];
    const res = [];
    while(queue.length) {
        let tmp = [];
        let size = queue.length;
        for(let i = 0; i < size; i++) {
            const node = queue.pop();
            tmp.push(node.val);
            node.left && queue.unshift(node.left);
            node.right && queue.unshift(node.right);
        }
        res.push(tmp)
    }
    return res;
};
```