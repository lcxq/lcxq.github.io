---
title: leetcode No.9 回文数
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-18 19:47:29
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 回文数

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例 1:**

```markdown
输入: 121
输出: true
```

**示例 2:**

```markdown
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3:**

```markdown
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

进阶:

你能不将整数转为字符串来解决这个问题吗？

## 方法一

直接转换成string再调用reverse方法，equals判断

```java
class Solution {
    public boolean isPalindrome(int x) {
        StringBuilder str = new StringBuilder();
        str.append(x);
        return str.toString().equals(str.reverse().toString());
    }
}
```

## 方法二

官方题解给出的解法，只要反转一半的数字判断是否相等即可

```java
class Solution {
    public boolean isPalindrome(int x) {
        // 先去除特殊情况
        // 1) x为负数 2) x末尾为0但自身不为0(x不可能以0开头，除非本身就是0)
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }
        int retNumber = 0;
        while (x > retNumber) {
            retNumber = retNumber * 10 + x % 10;
            x /= 10;
        }
        //分奇偶数情况，如果位数为奇数则retNumber会多一位中间位，但中间位数字不影响回文
        return x == retNumber || x == retNumber / 10;
    }
}
```
