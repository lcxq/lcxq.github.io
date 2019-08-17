---
title: leetcode No.5 最长回文子串
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-17 00:45:57
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

**示例 1：**

```markdown
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```

**示例 2：**

```markdown
输入: "cbbd"
输出: "bb"
```

在准备复试上机研究动态规划时碰到过该题，法一就按照《算法笔记》中给出的解法解题

## 方法一

![状态转移方程](https://s2.ax1x.com/2019/08/17/muADmQ.png)

根据子串长度进行遍历，L = 3 to s.len 其中L=1,2在初始化部分遍历完毕

```java

class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        String str = "";
        int ans = 0;
        int [][] dp = new int [len][len];
        for (int i = 0; i < len; i++) {
            dp[i][i]=1;
            if( ans==0 ){
                str = s.substring(i, i+1);
                ans = 1;
            }
            if(i<len-1 && s.charAt(i)==s.charAt(i+1)){
                dp[i][i+1] = 1;
                if(ans < 2){
                    str = s.substring(i, i+2);
                    ans = 2;
                }
            }
        }
        for(int L=3; L<=len;L++){
            for(int i =0;i+L-1<len;++i){
                int j =i + L -1;
                if(s.charAt(i)==s.charAt(j) && dp[i+1][j-1]==1){
                    dp[i][j]=1;
                    if(L > ans){
                        str = s.substring(i, j+1);
                        ans = L;
                    }
                }
            }
        }
        return str;
    }
}
```

**时间复杂度：**
$$O(n^2)$$
**空间复杂度：**
$$O(n^2)$$

## 方法二

官方题解给出的中心扩展算法，思路很简单，遍历每一个可能成为回文子串的中心点(可能是奇数子串的中间字符，也可能是偶数子串的中间间隙)

每次遍历向两边扩展搜寻回文串即可，返回遍历过程的最长回文子串。

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length()==0) return "";
        String resultString = s.substring(0, 1);
        for(int i =0;i<s.length()-1;++i){
            String str1 = centerExpand(s, i, i);
            String str2 = centerExpand(s, i, i+1);
            String max_String = (str1.length()>str2.length())?str1:str2;
            if(resultString.length()<max_String.length()){
                resultString = max_String;
            }
        }
        return resultString;
    }
    private String centerExpand(String s, int left, int right) {
        int L = left, R = right;
        while(L>=0 && R < s.length() && s.charAt(L)==s.charAt(R)){
            L--;
            R++;
        }
        return s.substring(L+1, R);//这里要注意，循环退出时，R和L指向最近的不回文字符，因此要各回退一位
    }
}
```

**时间复杂度：**
$$O(n^2)$$
**空间复杂度：**
$$O(n)$$

## 方法三

Manacher 算法

以后有机会再补这个算法
