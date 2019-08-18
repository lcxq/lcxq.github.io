---
title: leetcode No.7 整数反转
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-18 15:23:55
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 整数反转

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

**示例1：**

```markdown
输入: 123
输出: 321
```

**示例2：**

```markdown
输入: -123
输出: -321
```

**示例3：**

```markdown
输入: 120
输出: 21
```

**注意：**

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

## 方法

比较简单的题，输入的数字一边对10取余，一边把余数乘10加入待返回数字即可，迭代过程中判断一下当前数字是否越界

```java
class Solution {
    public int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
            if (rev < Integer.MIN_VALUE/10 || (rev == Integer.MIN_VALUE/10 && pop < -8)) return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
}
```
