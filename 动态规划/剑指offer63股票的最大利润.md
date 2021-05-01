## 题目
假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

[连接](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

TAG: 中等

## 解决方案

将问题划分为昨天的最大利润与卖掉今天的股票得到的利润相比

```javascript
var maxProfit = function(prices) {
    if (prices.length === 0) return 0;
    const dp = [0];
    let lowCost = prices[0];
    for(let i = 1; i < prices.length; i++) {
        if (lowCost > prices[i]) lowCost = prices[i];
        dp[i] = Math.max(dp[i - 1], prices[i] - lowCost);
    }
    return dp[prices.length - 1];
};
```