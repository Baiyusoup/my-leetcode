## 题目
给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

[来源](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof)

TAG: 简单

## 解题思路
对于二叉树的搜索，无非就三种：前序遍历、中序遍历和后序遍历。
分析一下题目，根据题意总共有四种情况
1. p和q分别处于x节点的左右子树中
2. p是x节点，而q是在某个子树中
3. q是x节点，而p是在某个子树中
4. p和q都在x节点的某个子树中

然后我们在进一步分析，可以将上述情况划分为p或q是x节点，q和p处于x的子树中。
对于第一种情况，当我们知道p或q是x节点的时候，那么这个q或p就是一个最近公共祖先节点，这样的话我们就不需要进一步访问子树了，我们已经找到最近公共祖先了，将它返回就行了。

对于第二种情况，如何知道p或q是处在x的子树呢？因为二叉树的遍历都是递归的，而且在第一种情况中，我们知道是有返回值的，而且二叉树的遍历的终止条件是当前节点为null，那么我们就可以判断返回值是null还是一个节点了。

如果为null，那肯定是遍历完当前节点的某棵子树都找不到p或q节点，因此我们就知道在另一颗子树上肯定能找到q或p，我们将那一颗子树返回就行了，那棵子树节点就是一个最近公共祖先。

如果不为null，那么q或p节点肯定在这颗子树上，将这颗子树返回即可。

```javascript
var lowestCommonAncestor = function(root, p, q) {
    // 递归终止条件
    if(root === null) return null;
    // root是q或p
    if (root === p) return root;
    if (root === q) return root;

    // 判断当前节点的哪棵子树存在p或q节点
    let left = lowestCommonAncestor(root.left, p, q);
    let right = lowestCommonAncestor(root.right, p, q);

    if (left === null) {
      // 右子树存在p或q
        return right;
    } else if (right === null) {
      // 左子树存在p或q
        return left;
    } else {
      // 左右子树分别有qp节点
        return root;
    }
};
```