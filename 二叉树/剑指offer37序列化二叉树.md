题目要求我们实现两个函数来分别序列化和反序列化二叉树

根据它给的例子，我想到的是bfs来序列化，对于反序列化也是通过bfs的思路来实现

[连接](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)


```javascript

/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */

var serialize = function(root) {
    if (root === null) return '';
    const stack = [root];
    const res = [];
    while(stack.length) {
        const node = stack.shift();
        if (node) {
            stack.push(node.left);
            stack.push(node.right);
        }
        res.push(node ? node.val : null);
    }
    return res.toString();
};

var deserialize = function(data) {
    if (data.length === 0) return null;
    const tree = data.split(",");
    const root = new TreeNode(tree.shift());
    const stack = [root];
    while (tree.length) {
        const node = stack.shift();
        const left = tree.shift();
        const right = tree.shift();

        if (left === '') {
            node.left = null;
        } else {
            node.left = new TreeNode(left);
            stack.push(node.left);
        }

        if (right === '') {
            node.right = null;
        } else {
            node.right = new TreeNode(right);
            stack.push(node.right);
        }
    }
    return root;
};
```