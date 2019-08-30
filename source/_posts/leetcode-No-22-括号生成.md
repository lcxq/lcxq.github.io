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
        generateAll("", res, n);
        return res;
    }
    private void generateAll(String cur, List<String> res, int n) {
        if (cur.length() == 2 * n) {
            if (valid(cur)) {
                res.add(cur);
            }
        } else {
            generateAll(cur + '(', res, n);
            generateAll(cur + ')', res, n);
        }
    }
    private boolean valid(String cur) {
        int balance = 0;
        for (char c : cur.toCharArray()) {
            if (c == '(') {
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

容易发现，生成括号的数量直接决定了序列是否有效，因此可以通过控制左右括号生成的数量来生成合法序列。

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        generateAll("", 0, 0, res,n);
        return res;
    }
    private void generateAll(String cur, int left, int right, List<String> res, int n) {
        if (cur.length() == 2 * n) {
            res.add(cur);
        } else {
            if (left < n) generateAll( cur + '(', left + 1, right, res, n);
            if (right < left) generateAll(cur + ')', left, right + 1, res, n);
        }
    }
}
```

## 方法三

每个合法序列实际上都可以分割为左子序列和右子序列，迭代分割位点即可得到所有序列

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> ans = new ArrayList();
        if (n == 0) {
            ans.add("");
        } else {
            for (int a = 0; a < n; a++)
                for (String left: generateParenthesis(a))
                    for (String right: generateParenthesis(n-1-a))
                        ans.add("(" + left + ")" + right);
        }
        return ans;
    }
}
```
