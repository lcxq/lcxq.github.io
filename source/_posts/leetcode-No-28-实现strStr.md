---
title: leetcode No.28 实现strStr
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-02 22:16:23
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 实现strStr()

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

**示例 1:**

```markdown
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```markdown
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

## 方法

字符串匹配问题，暴力肯定是最简单的

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        for (int i = 0; i < haystack.length() - needle.length() + 1; i++) {
            int index1 = i, index2 = 0;
            boolean ismatched = true;
            while (index1 < haystack.length() && index2 < needle.length()) {
                if (haystack.charAt(index1++) != needle.charAt(index2++)) {
                    ismatched = false;
                    break;
                }
            }
            if (ismatched) return i;
        }
        return -1;
    }
}
```

这题没必要再去复习一下KMP算法吧？。。。。。
