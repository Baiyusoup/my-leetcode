## 题目
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

[连接](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

TAG: 简单

## 解决方案

hash表
```javascript
var firstUniqChar = function(s) {
  if(s.length === 0) return " ";
  const map = new Map();
  for(let c of s) {
      map.set(c, !map.has(c));
  }
  for(let kv of map.entries()) {
      if (kv[1]) return kv[0];
  }
  return " ";
};
```

```java
class Solution {
    public char firstUniqChar(String s) {
      // 有序hash
      Map<Character, Boolean> dic = new LinkedHashMap<>();
      char[] sc = s.toCharArray();
      for(char c: sc) {
        dic.put(c, !dic.containsKey(c));
      }
      for(Map.Entry<Character, Boolean> d: dic.entrySet()) {
        if (d.getValue()) return d.getKey();
      }
      return " ";
    }
}
```
两次循环完成，因此时间O(N)，因为只含小写字母，因此hash表最大为26个，因此O(1)

