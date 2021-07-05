[链接](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

题目要求写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)），且答案要取模1000000007。

斐波那契数列是一个典型的动态规划基础题，因此它的状态转移方程为F(N) = F(N - 1) + F(N - 2)，初始状态F(0) = 0,   F(1) = 1。

如果使用递归处理，会有很多重复的计算，因此可通过记忆化的方式保存已经计算过的状态。又因为Fn只和n-1和n-2这两个状态有关，因此可以使用a、b来保存状态，同时用辅助遍历sum来是ab两个状态交替前进。空间复杂度降低为O（1）

```javascript
function fib(n) {
  let a = 0, b = 1, sum;
  for(let i = 0; i < n; i++) {
    sum = (a + b) % 1000000007;
    a = b;
    b = sum;
  }
  return a;
}
```