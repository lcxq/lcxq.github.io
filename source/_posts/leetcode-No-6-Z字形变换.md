---
title: leetcode No.6 Z字形变换
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-17 21:35:09
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# Z字形变换

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：

```markdown
L   C   I   R
E T O E S I I G
E   D   H   N
```

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：

```markdown
string convert(string s, int numRows);
```

**示例 1:**

```markdown
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
```

**示例 2:**

```markdown
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

L     D     R
E   O E   I I
E C   I H   N
T     S     G
```

## 方法一

找规律，首先计算Z字形相同行数的周期 T ，发现 T = 2 * row - 2

即首排和尾排可以按照 i += 2 * row 搜索下一个字符

中间排每个周期要输出两个字符，前一个 i += T - 2 * row

后一个 i += 2 * row

```java
class Solution {
    public String convert(String s, int numRows) {
        int T = 2*numRows -2;
        String result = "";
        if(numRows==1) return s;
        for (int row = 0; row < numRows; row++) {
            boolean flag = true;
            int index = row;
            if(row == 0 || row == numRows-1){
                while (index < s.length()) {
                    result += s.charAt(index);
                    index += T;
                }
            }else{
                while (index < s.length()) {
                    result += s.charAt(index);
                    if(flag){
                        index += T - 2 * row;
                    }else{
                        index += 2 * row;
                    }
                    flag = !flag;
                }
            }
        }
        return result;
    }
}
```

**时间复杂度：**
把整个字符串遍历一遍，即
$$O(n)$$

该方法可以根据官方题解进一步简化代码（优化中间排的搜索思路

同时改用StringBuilder类创建字符串避免大量拼接操作导致产生冗余的中间对象

```java
class Solution {
    public String convert(String s, int numRows) {
        if(s.length() <= numRows || numRows == 1) return s;
        StringBuilder result = new StringBuilder();
        int T = 2 * numRows - 2;
        for (int i = 0; i < numRows; i++) {
            for (int j = 0; j + i < s.length(); j += T) {
                result.append(s.charAt(j + i));
                if( i != 0 && i != numRows - 1 && j + T - i < s.length()) {
                    result.append(s.charAt(j + T - i));
                }
            }
        }
        return result.toString();
    }
}
```

## 方法二

官方题解给出的方法，本质和二维数组差不多

```java
class Solution {
    public String convert(String s, int numRows) {

        if (numRows == 1) return s;

        List<StringBuilder> rows = new ArrayList<>();
        for (int i = 0; i < Math.min(numRows, s.length()); i++)
            rows.add(new StringBuilder());

        int curRow = 0;
        boolean goingDown = false;

        for (char c : s.toCharArray()) {
            rows.get(curRow).append(c);
            if (curRow == 0 || curRow == numRows - 1) goingDown = !goingDown;
            curRow += goingDown ? 1 : -1;
        }

        StringBuilder ret = new StringBuilder();
        for (StringBuilder row : rows) ret.append(row);
        return ret.toString();
    }
}
```

但该方法反复读取list中的对象且开辟了类二维数组，时间和空间花费较多。
