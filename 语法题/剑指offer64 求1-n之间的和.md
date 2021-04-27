## 题目
求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

[连接](https://leetcode-cn.com/problems/qiu-12n-lcof/solution/)

TAG: 简单

## 解决方案
题目就给我们限制死了，摆明了让我们用递归。递归肯定要有终止嘛，不能用if这些，就只能使用短路运算了

在js中，你不能 false && return x，因为return没有返回值，所以不能那么写。

然后再想想，在js中，0就是false，非0就是true，数字和布尔值相加，是会进行隐式转换的，布尔值会转换成对象的数字，那么我们就利用这个性质

```javascript
var sumNums = function(n) {
    return !(n - 1) || (n + sumNums(n - 1))
};
```