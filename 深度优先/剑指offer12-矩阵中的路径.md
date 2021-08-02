```javascript
function exist(board, word) {
  const R = board.length, C = board[0].length
  const dfs = (i, j, k) => {
    if (
      !(i >= 0 && i < R) ||
      !(j >= 0 && j < C) ||
      board[i][j] !== word[k]
    ) {
      return false
    }
    if (k === word.length - 1) return true
    board[i][j] = ''
    res = dfs(i + 1, j, k + 1) || dfs(i - 1, j, k + 1) || dfs(i, j + 1, k + 1) || dfs(i, j - 1, k + 1)
    board[i][j] = word[k]
    return res
  }

  
}
```