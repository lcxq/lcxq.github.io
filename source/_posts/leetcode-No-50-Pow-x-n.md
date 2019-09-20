---
title: 'leetcode No.50 Pow(x,n)'
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-20 17:42:37
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# Pow(x,n)

实现 *pow(x, n)* ，即计算 x 的 n 次幂函数。

**示例 1:**

    输入: 2.00000, 10
    输出: 1024.00000

**示例 2:**

    输入: 2.10000, 3
    输出: 9.26100

**示例 3:**

    输入: 2.00000, -2
    输出: 0.25000
    解释: 2-2 = 1/22 = 1/4 = 0.25

**说明:**

* -100.0 < x < 100.0
* n 是 32 位有符号整数，其数值范围是 [−2<sup>31</sup>,  2<sup>31</sup> − 1] 。

## 方法一

采用递归的方式，思想和No.29类似，可以让乘数不断翻倍来降低时间复杂度

```java
class Solution {
    public double powRecursion(double x, int n) {
        if (n == 0) return 1;
        //偶数的情况
        if ((n & 1) == 0) {
            double temp = powRecursion(x, n / 2);
            return temp * temp;
        } else { //奇数的情况
            double temp = powRecursion(x, n / 2);
            return temp * temp * x;
        }
    }
    public double myPow(double x, int n) {
        if (x == -1) {
            if ((n & 1) != 0) return -1;
            else return 1;
        }
        if (x == 1.0f) return 1;
        if (n == -2147483648) return 0;
        double mul = 1;
        if (n > 0) mul = powRecursion(x, n);
        else {
            n = -n;
            mul = powRecursion(x, n);
            mul = 1 / mul;
        }
        return mul;
    }
}
```

## 方法二

迭代算法。非常巧妙，将指数看成二进制，遍历其位数来实现二分的迭代。

```java
class Solution {
    public double myPow(double x, int n) {
        if (x == -1) {
            if ((n & 1) != 0) {
                return -1;
            } else {
                return 1;
            }
        }
        if (x == 1.0f)
            return 1;
        if (n == -2147483648) {
            return 0;
        }
        double mul = 1;
        if (n > 0) {
            mul = powIteration(x, n);
        } else {
            n = -n;
            mul = powIteration(x, n);
            mul = 1 / mul;
        }
        return mul;
    }
    public double powIteration(double x, int n) {
        double ans = 1;
        //遍历每一位
        while (n > 0) {
            //最后一位是 1，加到累乘结果里
            if ((n & 1) == 1) {
                ans = ans * x;
            }
            //更新 x
            x = x * x;
            //n 右移一位
            n = n >> 1;
        }
        return ans;
    }
}
```
