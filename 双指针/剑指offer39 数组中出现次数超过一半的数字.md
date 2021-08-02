## 题目
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。你可以假设数组是非空的，并且给定的数组总是存在多数元素。

[连接](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

TAG: 简单

## 解决方案

**哈希表统计**
使用hash表记录每个数字出现的次数，返回次数最多的数字即可

```javascript
var majorityElement = function(nums) {
    const hash = new Map();
    let maxI = nums[0], maxV = 1;
    nums.forEach((v, i) => {
        if (hash.has(v)) {
            hash.set(v, hash.get(v) + 1)
            if (hash.get(v) > maxV) {
                maxV = hash.get(v);
                maxI = v;
            }
        } else {
            hash.set(v, 1);
        }
    })
    return maxI;
};
```
因为hash表在最坏的情况下的大小为nums.length，算法是在一次遍历完成，因此时间和空间复杂度O(n)

**排序找中点数**
因为数组中的数有一个数字出现的次数超过数组长度的一半，因此排序后，最多的数字一定是在中间。

**摩尔投票法**
核心理念为 票数正负抵消 。此方法时间和空间复杂度分别为 O(N) 和 O(1) 

```javascript
var majorityElement = function(nums) {
    let votes = 0, x = 0;
    nums.forEach((v, i) => {
        votes === 0 && x = v;
        votes += x === v ? 1 : -1;
    })
    return x;
};
```

摩尔投票法使用场景是找出占半数以上的那类东西，简单来说就是不同的东西就会相互抵消，那么到最后剩下来的肯定是数量占半数以上的那类东西

