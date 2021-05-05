## 题目
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

[连接](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

TAG: 简单

## 解决方案

根据定义:
- 左子树L的根节点和右子树R的根节点的值相等
- L.left.val = R.right.val
- L.right.val = R.left.val

根据以上规律，考虑从顶至底递归，判断每对节点是否对称，从而判断树是否为对称二叉树

定义recur(L, R)函数来判断当前节点是否对称

- 终止条件
  - 当L和R同时为null时，表明此树从顶到底的节点都是对称的，返回true
  - 当L和R其中有一个不为null时，表明不对称，返回false
  - 当L和R的值不相等时，返回false

- 递归工作：判断当前L和R相应的子树是否相等

```javascript
var isSymmetry = function(root) {
  if (!root) return true;
  return recur(root.left, root.right);
}

function recur(L, R) {
  if(L === null && R === null) return true;
  if (L === null || R === null) return false;
  return recur(L.left, R.right) && recur(L.right, R.left) && L.val === R.val;
}
```