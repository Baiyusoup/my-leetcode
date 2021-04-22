## 题目
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到**叶节点**所经过的节点形成一条路径。

[连接](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

TAG: 中等

## 解决方案
先序遍历二叉树

定义一个数组记录路径，每访问一个节点，就将该节点放入路径数组中，如果减去当前节点的值后为0，且当前节点为叶节点，则将当前路径数组保存起来。当访问完当前节点的左右子树时，将当前节点从路径数组中删除。

```javascript
var pathSum = function(root, target) {
    if (!root) return [];
    const res = [];
    let path = [];
    function recur(root, tar) {
        if (!root) {
          return;
        }
        path.push(root.val);
        tar -= root.val;
        if (tar === 0 && !root.left && !root.right) {
            res.push([...path])
        }
        recur(root.left, tar);
        recur(root.right, tar);
        path.pop();
    }
    recur(root, target);
    return res;
};

```