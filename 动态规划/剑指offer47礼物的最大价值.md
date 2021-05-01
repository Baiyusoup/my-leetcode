## 题目
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？


[连接](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof)

TAG: 中等

## 解决方案
设f(i, j)为从棋盘左上角走到单元格(i,j)的礼物最大累计值，易得递推关系`f(i,j)=max(f(i+1,j), f(i,j+1)) + grid[i][j]`

- 状态定义：设动态矩阵`dp[i,j]`·代表从棋盘左上角开始，到达`grid[i][j]`时的最大累计值
- 状态转移方程
  1. 当i=0,j=0时，为起始元素
  2. i=0，j！=0时，只能从左边到达
  3. i！=0，j=0时，只可从上边到达
  4. i！=0，j!=0时，左边或上边都可到达

```javascript
function maxValue = function(grid) {
  let row = gird.length;
  let col = grid[0].length;
  for(let i = 0; i < row; i++) {
    for(let j = 0; j < col; j++) {
      if(i === 0 && j === 0) continue;
      if (i === 0) grid[i][j] += grid[i][j - 1];
      else if (j === 0) grid[i][j] += grid[i - 1][j];
      else grid[i][j]  += Math.max(grid[i][j-1], grid[i-1][j])
    }
  }
  return grid[row - 1][col - 1];
}
```