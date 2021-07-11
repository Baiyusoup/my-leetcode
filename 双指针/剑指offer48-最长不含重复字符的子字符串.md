[链接](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

两种解法
1. 动态规划
2. 双指针（滑动窗口）

```javascript
function lengthOfLongestSubstring(s) {
  // 哈希表
  const map = new Map();
  let i = -1, res = 0;
  for(let j = 0; j < s.length; j++) {
    // 判断是否存在哈希表中
    const ch = s[j];
    if (map.has(ch)) {
      i = Math.max(i, map.get(ch));
    }
    map.set(ch, j);
    res = Math.max(res, j - i);
  }
  return rs;                                                                                                                      
}
```