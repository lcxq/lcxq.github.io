---
title: leetcode No.36 有效的数独
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-11 12:44:51
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 有效的数独

判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

    1.数字 1-9 在每一行只能出现一次。

    2.数字 1-9 在每一列只能出现一次。

    3.数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

![数独](https://s2.ax1x.com/2019/09/11/ndMe2t.png)

上图是一个部分填充的有效的数独。

数独部分空格内已填入了数字，空白格用 '.' 表示。

**示例 1:**

```markdown
输入:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: true
```

**示例 2:**

```markdown
输入:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: false
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。
     但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。
```

**说明:**

    1.一个有效的数独（部分已被填充）不一定是可解的。

    2.只需要根据以上规则，验证已经填入的数字是否有效即可。

    3.给定数独序列只包含数字 1-9 和字符 '.' 。

    4.给定数独永远是 9x9 形式的。

## 方法一

自己写的暴力解法，能AC，分别遍历行，列和3*3矩阵判断是否有重复数字即可。

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        for (int i = 0; i < 9; i++) {
            HashMap<Integer, Integer> map = new HashMap<>();
            for (int j = 0; j < 9; j++) {
                if (board[i][j] == '.') continue;
                else {
                    int num = Character.getNumericValue(board[i][j]);
                    if (map.containsKey(num)) {
                        return false;
                    } else map.put(num, 1);
                }
            }
        }
        for (int i = 0; i < 9; i++) {
            HashMap<Integer, Integer> map = new HashMap<>();
            for (int j = 0; j < 9; j++) {
                if (board[j][i] == '.') continue;
                else {
                    int num = Character.getNumericValue(board[j][i]);
                    if (map.containsKey(num)) {
                        return false;
                    } else map.put(num, 1);
                }
            }
        }
        for (int i = 0; i < 9; i += 3) {
            for (int j = 0; j < 9; j += 3) {
                HashMap<Integer, Integer> map = new HashMap<>();
                for (int m = 0; m < 3; m++) {
                    for (int n = 0; n < 3; n++) {
                        if (board[i + m][j + n] == '.') continue;
                        else {
                            int num = Character.getNumericValue(board[i + m][j + n]);
                            if (map.containsKey(num)) {
                                return false;
                            } else map.put(num, 1);
                        }
                    }
                }
            }
        }
        return true;
    }
}
```

**时间复杂度：** $$O(3n)$$

## 方法二

参考了下官方题解，分别给列，行和子矩阵建立哈希表数组，可以只遍历一遍。

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        HashMap<Integer, Integer>[] rows = new HashMap[9];
        HashMap<Integer, Integer>[] columns = new HashMap[9];
        HashMap<Integer, Integer>[] boxes = new HashMap[9];
        for (int i = 0; i < 9; i++) {
            rows[i] = new HashMap<Integer, Integer>();
            columns[i] = new HashMap<Integer, Integer>();
            boxes[i] = new HashMap<Integer, Integer>();
        }
        for (int i = 0; i < 9; i++) {
            for (int j = 0; j < 9; j++) {
                if (board[i][j] != '.') {
                    int num = Character.getNumericValue(board[i][j]);
                    int box_index = (i / 3) * 3 + j / 3;
                    rows[i].put(num, rows[i].getOrDefault(num, 0) + 1);
                    columns[j].put(num, columns[j].getOrDefault(num, 0) + 1);
                    boxes[box_index].put(num, boxes[box_index].getOrDefault(num, 0) + 1);
                    if (rows[i].get(num) > 1 || columns[j].get(num) > 1 || boxes[box_index].get(num) > 1) {
                        return false;
                    }
                }
            }
        }
        return true;
    }
}
```

**时间复杂度：** $$O(n)$$
