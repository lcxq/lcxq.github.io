---
title: leetcode No.29 两数相除
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-03 13:19:01
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 两数相除

给定两个整数，被除数 dividend 和除数 divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 dividend 除以除数 divisor 得到的商。

**示例 1:**

```markdown
输入: dividend = 10, divisor = 3
输出: 3
```

**示例 2:**

```markdown
输入: dividend = 7, divisor = -3
输出: -2
```

说明:

被除数和除数均为 32 位有符号整数。
除数不为 0。
假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−2<sup>31</sup>,  2<sup>31</sup> − 1]。本题中，如果除法结果溢出，则返回 INT_MAX （2<sup>31</sup> − 1）。

## 方法

用累减的方法实现除法，被除数不断减去除数并计算减去的次数即可得到答案。

题目需要注意以下几个点

1. 除法结果会溢出的可能性只有一种，就是被除数为INT_MIN，除数为-1，单独讨论即可。

2. 因为整型范围正负数不对称，负数范围稍大，因此全部转换成负数进行运算，在运算前记录一下最后答案的正负在返回时添上符号即可。

3. 直接减的话会TLE，因此采用先指数增加除数到小于被除数的最大除数，同时增加的次数也指数增加。再用被除数减去增大后的除数可以大大降低时间复杂度。

```java
class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == Integer.MIN_VALUE && divisor == -1) return Integer.MAX_VALUE;
        if (divisor == 1) {
            return dividend;
        }
        if (divisor == -1) {
            return -dividend;
        }
        boolean isnegetive = false;
        if ((dividend < 0 && divisor < 0) || (dividend > 0 && divisor > 0)) {
            isnegetive = false;
        } else isnegetive = true;
        dividend = Math.min(dividend, -dividend);
        divisor = Math.min(divisor, -divisor);
        int res = 0;
        int t = 0, count = 0;
        while (dividend <= divisor) {
            t = divisor;
            count = 1;
            while (dividend <= t + t && t + t < 0) {
                t += t;
                count += count;
            }
            res += count;
            dividend -= t;
        }
        return isnegetive ? -res : res;
    }
}

```
