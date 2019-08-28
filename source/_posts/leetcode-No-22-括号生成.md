---
title: leetcode No.22 括号生成
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-28 23:38:37
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 括号生成


给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

例如，给出 n = 3，生成结果为：

```markdown
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## 方法一

暴力法解题，先递归生成所有可能的括号序列，再判断生成的序列是否有效

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        generateAll(new char[2 * n], 0, res);
        return res;
    }
    private void generateAll(char[] charArray, int index, List<String> res) {
        if (index == charArray.length) {
            if (valid(charArray)) {
                res.add(new String(charArray));
            }
        } else {
            charArray[index] = '(';
            generateAll(charArray, index + 1, res);
            charArray[index] = ')';
            generateAll(charArray, index + 1, res);
        }
    }
    private boolean valid(char[] charArray) {
        int balance = 0;
        for (char c : charArray) {
            if (c == '{') {
                balance ++;
            }else balance--;
            if (balance < 0) {
                return false;
            }
        }
        return (balance == 0);
    }
}
```

## 方法二

容易发现，生成括号的数量直接决定了