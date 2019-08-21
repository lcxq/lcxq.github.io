---
title: leetcode No.10 正则表达式匹配
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-19 19:43:20
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 正则表达式匹配

给你一个字符串 *s* 和一个字符规律 *p*，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。

```markdown
'.' 匹配任意单个字符
'*' 匹配零个或多个前面的那一个元素
```

所谓匹配，是要涵盖 整个 字符串 *s* 的，而不是部分字符串。

说明:

s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。

**示例 1:**

```markdown
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```

**示例 2:**

```markdown
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```

**示例 3:**

```markdown
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```

**示例 4:**

```markdown
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```

**示例 5:**

```markdown
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```

## 方法一

官方题解一，通过递归实现，具体思路看注释

```java
class Solution {
    public boolean isMatch(String s, String p) {
        if (p.isEmpty()) return s.isEmpty();    //递归终点
        boolean first_match = (!s.isEmpty() && (s.charAt(0) == p.charAt(0) || p.charAt(0) == '.')); //判断当前递归的第一个字符是否匹配
        if(p.length()>=2 && p.charAt(1) == '*'){ //遇到星号的情况，星号总会是当前递归模式串的第二个字符
            return (isMatch(s, p.substring(2)) || (first_match && isMatch(s.substring(1), p))); //两种情况，一种是直接删除模式串星号部分判断是否匹配（星号可以匹配零个字符），另一种是第一个字符始终匹配，则模式串不变，文本串前移一位继续匹配直到不匹配为止。若不匹配的话则直接回溯到前一层递归删除星号部分再观察是否匹配
        }else {
            return (first_match && isMatch(s.substring(1), p.substring(1))); //没星号的情况就正常匹配
        }
    }
}
```

## 方法二

动态规划

```java
class Solution {
    public boolean isMatch(String s, String p) {
        //定义dp数组，dp[i][j]指模式串第j个字符前的子串能否匹配文本串第i个字符前的子串（从1开始数）
        boolean dp[][] = new boolean[s.length() + 1][p.length() + 1];
        //i,j=0指空串，空串自然能匹配空串
        dp[0][0] = true;
        //从s的空子串开始初始化，此时只有*能匹配空串
        for(int i = 1; i <=p.length(); ++i){
            if(p.charAt(i - 1) == '*' && dp[0][i - 2]){
                dp[0][i] = dp[0][i - 2];
            }
        }
        //遍历模式串与文本串
        for(int i = 1; i <= s.length(); ++i){
            for(int j = 1; j <= p.length(); ++j){
                //情况1，字符能直接匹配，则当前位置匹配情况直接继承前一位的情况
                if(s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '.'){
                    dp[i][j] = dp[i - 1][j - 1];
                //若不能直接匹配则要讨论*的情况
                }else if(p.charAt(j - 1) == '*'){
                //在模式串当前字符为*，而且*前的字符与文本串当前字符无法匹配，则只能把模式串的星号部分看做空串才能匹配
                    if(s.charAt(i-1) != p.charAt(j - 2) && p.charAt(j - 2) !='.'){
                        dp[i][j] = dp[i][j - 2];
                //*前字符能匹配时，分三种情况，一种是匹配空串，一种是匹配一个字符，一种是匹配多个字符
                    }else{
                        dp[i][j] = dp[i][j - 2] || dp[i][j - 1] || dp[i -1][j];
                        //经测试，可以把匹配一个字符的情况与多个字符的情况合并，如下
                        //dp[i][j] = dp[i][j - 2] || dp[i -1][j];
                    }
                }
            }
        }
        //返回数组最后的状态就是答案
        return dp[s.length()][p.length()];
    }
}
```
