---
title: leetcode No.37 解数独
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-11 22:56:35
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 解数独

编写一个程序，通过已填充的空格来解决数独问题。

一个数独的解法需**遵循如下规则**：

    1、数字 1-9 在每一行只能出现一次。

    2、数字 1-9 在每一列只能出现一次。

    3、数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

空白格用 '.' 表示。

![](https://s2.ax1x.com/2019/09/11/nwWfN8.png)

一个数独。

![](https://s2.ax1x.com/2019/09/11/nwW59g.png)

答案被标成红色。

**Note:**

    1、给定的数独序列只包含数字 1-9 和字符 '.' 。

    2、你可以假设给定的数独只有唯一解。

    3、给定数独永远是 9x9 形式的。

## 方法

回溯法，和走迷宫感觉差不多，本质上也可以看成DFS

```java
class Solution {
    public void solveSudoku(char[][] board) {
        solver(board);
    }
    private boolean solver(char[][] board){
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') {
                    char count = '1';
                    while (count <= '9') {
                        if (isValid(i, j, board, count)) {
                            board[i][j] = count;
                            if (solver(board)) {
                                return true;
                            } else {
                                board[i][j] = '.';
                            }
                        }
                        count ++;
                    }
                    return false;
                }
            }
        }
        return true;
    }
    private boolean isValid(int row, int col, char[][] board, char c) {
        for (int i = 0; i < 9; i++) {
            if (board[row][i] == c) {
                return false;
            }
        }
        for (int i = 0; i < 9; i++) {
            if (board[i][col] == c) {
                return false;
            }
        }
        int start_row = row / 3 * 3;
        int start_col = col / 3 * 3;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[start_row + i][start_col + j] == c) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
