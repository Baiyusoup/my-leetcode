## 题目
在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

[连接](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

TAG: 中等

## 解决方案

hash
```javascript
var singleNumber = function(nums) {
    const map = new Map();
    let res = 0;
    nums.forEach((v, i) => {
        if (map.has(v)) {
            map.set(v, map.get(v) + 1);
        } else {
            map.set(v, 1);
        }
    })
    for(let kv of map.entries()) {
        if (kv[1] === 1) return kv[0];
    }
};
```
时间/空间复杂度都为O(N)

