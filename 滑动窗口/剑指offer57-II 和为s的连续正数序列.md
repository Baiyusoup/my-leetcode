## 题目
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。


[连接](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

TAG: 简单

## 解决方案

**方法一：滑动窗口（枚举+暴力）**
枚举每个正整数为起点，判断将target减去当前正整数时是否为0即可，由于题目要求序列长度至少大于2，因此枚举的上界为target / 2。

```javascript
var findContinuousSequence = function(target) {
  let left = 1;
  let right = 1;
  let sum = 0;
  let res = [];
  let limit = Math.floor(target / 2);
  while(left <= limit) {
    if (sum < target) {
      sum += right;
      right++;
    } else if (sum > target) {
      sum -= left;
      left++;
    } else {
      let tmp = [];
      for(let k = left; k < right; k++) {
        tmp.push(k)
      }
      res.push(tmp)
      sum -= left;
      left++;
    }
  }
  return res;
}
```

**方法二：在一的基础上进行数学优化**
我们通过题意要求：一段连续整数之和等于target，我们的工作就是找出这一段连续的整数，转换程数学问题就是等差数列的求和。

$$
\frac{(起点+终点) * (终点 - 起点 + 1)}{2} = target
$$

因此就变成了解方程，一个关于起点的一元二次方程，套用求根公式即可。

需要注意得到的终点是否为整数
1. 判别式开根需要为整数
2. 最后求根公式的分子需要为偶数，因为分母为2

```javascript
var findContinuousSequence = function(target) {
    const res = [];
    let sum = 0, limit = Math.floor(target / 2);
    for(let x = 1; x <= limit; ++x) {
      let delta = 1 - 4 * (x - x * x - 2 * target);
      if (delta < 0) continue;

      let delta_sqrt = Math.floor(Math.sqrt(delta));
      let a = delta_sqrt * delta_sqrt === delta;
      let b = !((delta_sqrt - 1) & 1);
      if (a && b) {
      let y = Math.floor((-1 + delta_sqrt) / 2);
      if (x < y) {
        let tmp = [];
        for(let k = x; k <= y; k++) {
        tmp.push(k)
        }
        res.push(tmp)
      }
    }
  }
  return res;
}
```