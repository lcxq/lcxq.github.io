---
title: leetcode No.12 罗马数字转整数
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-22 22:13:11
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 罗马数字转整数

题目描述和上一道题几乎一样，就是输入输出反一反

## 方法

就和上一题差不多的实现方法做就好了。

```java
class Solution {
    public int romanToInt(String s) {
        int[] nums = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
        String[] strs = {"M", "CM", "D", "CD","C","XC","L","XL","X","IX","V","IV","I"};
        int result = 0, index = 0;
        for (int i = 0; i < strs.length; i++) {
            while(index < s.length() && s.substring(index, index + 1).equals(strs[i])){
                result += nums[i];
                index ++;
            }
            while(index + 1 < s.length() && s.substring(index, index + 2).equals(strs[i])){
                result += nums[i];
                index += 2;
            }
        }
        return result;
    }
}
```
