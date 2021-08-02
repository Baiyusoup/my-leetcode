## 题目
输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

[连接](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

TAG: 简单

## 解决方案

hash表
```javascript
var twoSum = function(nums, target) {
    const map = new Map();
    for(let i = 0; i < nums.length; i++) {
        if (map.has(nums[i])) {
            return [map.get(nums[i]), nums[i]];
        } else {
            map.set(target - nums[i], nums[i]);
        }
    }
    return [];
};
```

**双指针**
因为序列是递增序列，因此我们可以采用双指针，一头一尾。将两指针指向的值相加
- 如果结果 < target，头指针向前移
- 结果 > target，尾指针向后移
- 相等，结束

```javascript
var twoSum = function(nums, target) {
    let L = 0, R = nums.length - 1;
    while(L < R) {
        let res = nums[R] + nums[L];
        if (res < target) {
            L += 1;
        } else if (res > target) {
            R -= 1
        } else {
            return [nums[L], nums[R]]
        }
    }
    return [];
};
```
将空间复杂度降至O(1)

**一些细节**

if的条件判断可以改成 `target - nums[L]` 和 `nums[R]`比较，防止溢出的情况，同样在二分查找中，也是通过使用`left + ((right - left) >> 1)` 代替 (left + right) / 2
