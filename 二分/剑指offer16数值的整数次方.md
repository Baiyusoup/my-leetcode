题目要求实现pow(x, n)

求解思路有两个：
1. 通过循环将n个x乘起来，时间复杂度为O(n)
2. 快速幂法，时间复杂度O(logn)

```javascript
function myPow(x, n) {
  let res = x;
  let i = 0;
  while(true) {
    x = x*
    if (n&1) {
      
    }
    x = x*x;
  }
}
```

```javascript
function myPow(x, n) {
  if (n === 0) return 1;
  else if (n < 0) return 1/myPow(x, -n);
  else if (n&1) return x * myPow(x, n - 1);
  else return myPow(x*x, Math.floor(n / 2));
}
```