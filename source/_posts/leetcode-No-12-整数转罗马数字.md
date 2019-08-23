---
title: leetcode No.12 整数转罗马数字
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-22 17:33:57
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 整数转罗马数字

罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。

```markdown
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

- I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。

- X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。

- C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。

给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。

**示例 1:**

```markdown
输入: 3
输出: "III"
```

**示例 2:**

```markdown
输入: 4
输出: "IV"
```

**示例 3:**

```markdown
输入: 9
输出: "IX"
```

**示例 4:**

```markdown
输入: 58
输出: "LVIII"
解释: L = 50, V = 5, III = 3.
```

**示例 5:**

```markdown
输入: 1994
输出: "MCMXCIV"
解释: M = 1000, CM = 900, XC = 90, IV = 4.
```

## 方法一

分类讨论+递归处理数字即可

```java
class Solution {
    public String intToRoman(int num) {
        StringBuilder result = new StringBuilder();
        return deal(num, result);
   }
   private String deal(int num, StringBuilder result) {
           if(num >= 1000){
               result.append('M');deal(num - 1000, result);
           }else if(num >= 900){
               result.append("CM");deal(num - 900, result);
           }else if(num >= 500){
               result.append('D');deal(num - 500, result);
           }else if(num >= 400){
               result.append("CD");deal(num - 400, result);
           }else if(num >= 100){
               result.append('C');deal(num - 100, result);
           }else if(num >= 90){
               result.append("XC");deal(num - 90, result);
           }else if(num >= 50){
               result.append('L');deal(num - 50, result);
           }else if(num >= 40){
               result.append("XL");deal(num - 40, result);
           }else if(num >= 10){
               result.append("X");deal(num - 10, result);
           }else if(num >= 9){
               result.append("IX");deal(num - 9, result);
           }else if(num >= 5){
               result.append("V");deal(num - 5, result);
           }else if(num >= 4){
               result.append("IV");deal(num - 4, result);
           }else if(num >= 1){
               result.append('I');deal(num - 1, result);
           }
       return result.toString();
   }
}
```

## 方法二

[liweiwei1419](https://leetcode-cn.com/problems/integer-to-roman/solution/tan-xin-suan-fa-by-liweiwei1419/)的方法,属于贪心的思想，大致解法思路和方法一差不多，将递归改为迭代。

```java
class Solution {
    public String intToRoman(int num) {
        StringBuilder result = new StringBuilder();
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] strs = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};

        for (int i = 0; i < values.length; i++) {
            while(num >= values[i]){
                num -= values[i];
                result.append(strs[i]);
            }
        }
        return result.toString();
   }
}
```
