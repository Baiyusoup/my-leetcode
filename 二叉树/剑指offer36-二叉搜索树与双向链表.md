[链接](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

使用dfs(cur)中序遍历访问树，算法流程为
1. 终止条件为cur为空，直接返回
2. 递归左子树dfs(cur.left);
3. 构建链表
   1. 当pre为空时，代表正在访问链表头节点
   2. 当pre不为空时，修改双向节点引用，即pre.right = cur, cur.left = pre;
   3. 保存cur，即更新pre = cur
4. 递归右子树

treeToDoublyList(root)
1. 如果root为空，直接返回
2. 初始化，空节点pre
3. 转为双向链表：调用dfs(root);
4. 构建循环链表，中序遍历完后，head指向头节点，pre指向尾节点
5. 返回head


```javascript
var treeToDoublyList = function(root) {
  if (!root) return null;
  // 定义递归函数，创建双向链表
  const dfs = cur => {
    if (!cur) return;
    dfs(cur.left);
    if (pre) {
      // 修改两个相邻节点的指向
      head.right = pre;
      pre.left = head;
    } else {
      // pre == null 表明cur为头节点，最小的那个
      head = cur;
    }
    // 更新前驱
    pre = cur;
    dfs(cur.right);
  }
  
  // 初始化，pre为cur的前驱
  let pre = null, head;
  dfs(root);

  // 将头节点head和尾节点连接起来
  head.left = pre;
  pre.right = head;
  return head;
};
```
