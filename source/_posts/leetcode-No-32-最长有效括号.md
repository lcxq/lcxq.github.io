---
title: leetcode No.32 最长有效括号
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-06 17:15:06
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 最长有效括号

给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

**示例 1:**

```markdown
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```

**示例 2:**

```markdown
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```

## 方法一

优化暴力法，两重循环 i , j，但内层循环 j 不从头开始，而从 i + 1 开始，即判断从每个位置开始的最长合法子串是多长即可。

```java
class Solution {
    public int longestValidParentheses(String s) {
        int count = 0;
        int max = 0;
        for (int i = 0; i < s.length(); i++) {
            count = 0;
            for (int j = i; j < s.length(); j++) {
                if (s.charAt(j) == '(') {
                    count++;
                } else {
                    count--;
                }
                //count < 0 说明右括号多了，此时无论后边是什么，一定是非法字符串了，所以可以提前结束循环
                if (count < 0) {
                    break;
                }
                //当前是合法序列，更新最长长度
                if (count == 0) {
                    if (j - i + 1 > max) {
                        max = j - i + 1;
                    }
                }
            }
        }
        return max;
    }
}
```

**时间复杂度：** $O(n^2)$
**空间复杂度：** $O(1)$

## 方法二

动态规划，思路有点小复杂。 详情可见[这个大佬](https://leetcode.wang/leetCode-32-Longest-Valid-Parentheses.html)

```java
class Solution {
    public int longestValidParentheses(String s) {
        int maxans = 0;
        int dp[] = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                //右括号前边是左括号
                if (s.charAt(i - 1) == '(') {
                    dp[i] = (i >= 2 ? dp[i - 2] : 0) + 2;
                //右括号前边是右括号，并且除去前边的合法序列的前边是左括号
                } else if (i - dp[i - 1] > 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + ((i - dp[i - 1]) >= 2 ? dp[i - dp[i - 1] - 2] : 0) + 2;
                }
                maxans = Math.max(maxans, dp[i]);
            }
        }
        return maxans;
    }
}
```

**时间复杂度：** $O(n)$
**空间复杂度：** $O(n)$

## 方法三

借助栈，经过分析我们知道，该题的一个关键点在于遍历到右括号时需要已经出现过的左括号的位置信息，用栈记录左括号的位置即可。

```java
class Solution {
    public int longestValidParentheses(String s) {
        int maxans = 0;
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.empty()) {
                    stack.push(i);
                } else {
                    maxans = Math.max(maxans, i - stack.peek());
                }
            }
        }
        return maxans;
    }
}
```

**时间复杂度：** $O(n)$
**空间复杂度：** $O(n)$

## 方法四

很巧妙的方法，一开始自己分析由于只想到正向遍历结果没法解决类似“(((()”这样的问题因为遍历结束后记录括号的balance变量无法归零。实际上再反向遍历一遍就能解决这个问题。

```java
class Solution {
    public int longestValidParentheses(String s) {
        int left = 0, right = 0, maxlength = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                left++;
            } else {
                right++;
            }
            if (left == right) {
                maxlength = Math.max(maxlength, 2 * right);
            } else if (right >= left) {
                left = right = 0;
            }
        }
        left = right = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            if (s.charAt(i) == '(') {
                left++;
            } else {
                right++;
            }
            if (left == right) {
                maxlength = Math.max(maxlength, 2 * left);
            } else if (left >= right) {
                left = right = 0;
            }
        }
        return maxlength;
    }
}
```

**时间复杂度：** $O(n)$
**空间复杂度：** $O(1)$
