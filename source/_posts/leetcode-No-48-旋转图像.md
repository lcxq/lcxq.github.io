---
title: leetcode No.48 旋转图像
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-20 13:10:07
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 旋转图像

给定一个 n × n 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

**说明：**

你必须在**原地**旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

**示例 1:**

    给定 matrix =
    [
    [1,2,3],
    [4,5,6],
    [7,8,9]
    ],

    原地旋转输入矩阵，使其变为:
    [
    [7,4,1],
    [8,5,2],
    [9,6,3]
    ]

**示例 2:**

    给定 matrix =
    [
    [ 5, 1, 9,11],
    [ 2, 4, 8,10],
    [13, 3, 6, 7],
    [15,14,12,16]
    ],

    原地旋转输入矩阵，使其变为:
    [
    [15,13, 2, 5],
    [14, 3, 4, 1],
    [12, 6, 8, 9],
    [16, 7,10,11]
    ]

## 方法

看了半天没找出啥规律，直接看答案了。

其实两步操作就可以完成旋转。

    1、按照对角线翻转
    
    2、再按中轴线翻转

之后的实现就很简单了

```java
class Solution {
    public void rotate(int[][] matrix) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = i; j < matrix.length; j++) {
                if (i != j) {
                    int temp = matrix[i][j];
                    matrix[i][j] = matrix[j][i];
                    matrix[j][i] = temp;
                }
            }
        }
        for (int i = 0, j = matrix.length - 1; i < matrix.length / 2; i++, j--) {
            for (int k = 0; k < matrix.length; k++) {
                int temp = matrix[k][i];
                matrix[k][i] = matrix[k][j];
                matrix[k][j] = temp;
            }
        }
    }
}
```
