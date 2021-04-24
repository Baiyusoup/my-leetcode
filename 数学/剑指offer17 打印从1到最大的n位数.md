## 题目
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

[连接](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

TAG: 容易

## 解决方案

由数学知识知道最大的n位数位 10^n - 1;
```javascript
var printNumbers = function(n) {
    let res = [];
    for(let i = 1; i < 10**n; i++) {
        res.push(i)
    }
    return res;
};
```

但在实际面试中，很有可能会问你，如何处理超过32位的数呢？那么我们就需要考虑大数越界的问题了

对于大数的操作，我们一般是通过字符串来解决。

通过观察可知，生成的列表实际上是n位0-9的全排列（这个确实有点难想得到）

思路为通过分治算法的思想，先固定高位，向低位递归，当个位已被固定时，添加数字字符串。例如当n=2时，固定十位为0-9，按顺序依次开启递归，固定个位0-9，终止递归并添加数字字符串。

出现的问题：00、01、02这些结果。

- 字符串左边界定义：声明变量start规定字符串的左边界，以保证添加的数字字符串`num[start:]`中无高位多余0
- start变化规律：当输出数字的所有位都是9时，则下一个数字需要向更高位进1，此时左边界start需要减一，
- 统计nine的方法，固定第x位，当i=9时则执行nine++，并在回溯前恢复nine--

```javascript
var printNumbers = function(n) {
  let num = new Array(n).fill('0')
  let res = [];
  let start = n - 1;
  let nine = 0;
  function dfs(x) {
    if (x === n) {
      let s = num.splice(start).join('')
      if (s !== '0') res.push(s)
      if (n - start === nine) start -= 1;
      return
    }
    for(let i = 0; i < 10; i++) {
      if (i === 9) nine++；
      num[x] = i + '';
      dfs(x + 1)
    }
    nine--;
  }
  return res
};
```
好难理解。。。




