[链接](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

看到题目中的数组、递增序列字样，我脑子里第一想到的是二分查找，但是我没能写出来。

看了评论区，发现大神的思路是如此出奇：将二维数组逆时针转45°，问题就转变成在二叉搜索树中找元素！

真的令人惊叹，解法变成了如此简单！

```javascript
const findNumberIn2DArray = function(matrix, target) {
  // 如果matrix的长度为0，直接返回false
  if (matrix.length === 0) return false;
  const rLen = matrix.length, cLen = matrix[0].length;
  let i = rLen - 1, j = 0;
  while(i >= 0 && j < cLen) {
    const item = matrix[i][j];
    // 如果item < target, 说明目标元素在右子树
    if (item < target) {
      j++;
    } else if (item > target) {
      // item > target, 说明目标元素在左子树
      i--;
    } else {
      // 找到目标元素
      return true;
    }
  }
  return false;
}
```