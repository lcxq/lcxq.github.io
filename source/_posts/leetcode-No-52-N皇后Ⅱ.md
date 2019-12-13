---
title: leetcode No.52 N皇后Ⅱ
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-27 16:13:59
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

描述就不写了，和上一题几乎一样，知识最后返回可能的情况数而不是所有情况的棋盘，在递归终点的操作处略做修改即可。

```java
class Solution {
    int ans = 0;
    public int totalNQueens(int n) {
        dfs(n, new ArrayList<Integer>());
        return ans;
    }
    private void dfs(int n, List<Integer> currentQueen) {
        if (currentQueen.size() == n) {
            ans++;
            return;
        }
        for (int col = 0; col < n; col++) {
            if (!currentQueen.contains(col) && !isDiagonalAttack(currentQueen, col)) {
                currentQueen.add(col);
                dfs(n, currentQueen);
                currentQueen.remove(currentQueen.size() - 1);
            }
        }
    }
    private boolean isDiagonalAttack(List<Integer> currentQueen, int col) {
        int currentCol = col;
        int currentRow = currentQueen.size();
        for (int row = 0; row < currentRow; row++) {
            if (Math.abs(currentRow - row) == Math.abs(currentCol - currentQueen.get(row)) ) {
                return true;
            }
        }
        return false;
    }
}
```
