---
title: leetcode No.51 N皇后
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-27 16:00:58
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# N皇后

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

![八皇后](https://s2.ax1x.com/2019/09/27/uKwHoT.png)

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

**示例:**

    输入: 4
    输出: [
    [".Q..",  // 解法 1
    "...Q",
    "Q...",
    "..Q."],

    ["..Q.",  // 解法 2
    "Q...",
    "...Q",
    ".Q.."]
    ]
    解释: 4 皇后问题存在两个不同的解法。

## 方法

回溯法，和之前的几道回溯的题写法差不多。其中用一个一维list表示棋盘情况。

```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> ans = new ArrayList<>();
        dfs(ans, new ArrayList<Integer>(), n);
        return ans;
    }
    private void dfs(List<List<String>> ans, List<Integer> currentQueen, int n) {
        if (currentQueen.size() == n) {
            List<String> temp = new ArrayList<>();
            for (int i = 0; i < n; i++) {
                char[] ch = new char[n];
                Arrays.fill(ch, '.');
                ch[currentQueen.get(i)] = 'Q';
                temp.add(new String(ch));
            }
            ans.add(temp);
            return;
        } else {
            for (int col = 0; col < n; col++) {
                if (!currentQueen.contains(col) && !isDiagaolAttack(currentQueen, col)) {
                    currentQueen.add(col);
                    dfs(ans, currentQueen, n);
                    currentQueen.remove(currentQueen.size() - 1);
                }
            }
        }
    }
    private boolean isDiagaolAttack(List<Integer> currentQueen, int col) {
        int currentRow = currentQueen.size();
        int currentCol = col;
        for (int row = 0; row < currentRow; row++) {
            if (Math.abs(currentCol - currentQueen.get(row)) == Math.abs(currentRow - row)) {
                return true;
            }
        }
        return false;
    }
}
```
