---
title: leetcode No.14 最长公共前缀
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-23 11:45:07
password:
summary:
tags:
 - leetcode
 - 算法
 - Java 
categories: leetcode
---

# 最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

**示例 1:**

```markdown
输入: ["flower","flow","flight"]
输出: "fl"
```

**示例 2:**

```markdown
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

说明:

所有输入只包含小写字母 a-z 。

## 方法一

水平遍历

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        int min_length = Integer.MAX_VALUE;
        StringBuilder result = new StringBuilder();
        for (String str : strs) {
            min_length = Math.min(min_length, str.length());
        }
        if(strs.length==0) return "";
        for (int i = 0; i < min_length; i++) {
            for (int j = 0; j < strs.length; j++) {
                if(strs[j].charAt(i) != strs[0].charAt(i)){
                    return result.toString();
                }
            }
            result.append(strs[0].charAt(i));
        }
        return result.toString();
    }
}
```

## 方法二

分治法

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length==0) return "";
        else return(longestCommonPrefix(0, strs.length - 1, strs));

    }
    private String longestCommonPrefix(int left, int right, String[] strs) {
        if(left == right){
            return strs[left];
        }else{
            int mid = (left + right) / 2;
            String leftCommonPrefix = longestCommonPrefix(left, mid, strs);
            String rightCommonPrefix = longestCommonPrefix(mid + 1, right, strs);
            return commonPrefix(leftCommonPrefix, rightCommonPrefix);
        }
    }
    private String commonPrefix(String leftStr, String rightStr) {
        int index = 0;
        StringBuilder commonStr = new StringBuilder();
        while(index < leftStr.length() && index < rightStr.length()){
            if(leftStr.charAt(index) == rightStr.charAt(index)){
                commonStr.append(leftStr.charAt(index));
            }else break;
            index ++;
        }
        return commonStr.toString();
    }
}
```

## 方法三

二分法搜索第一个字符串的某一个位置，使得以这个位置为末尾的前缀子串最长且是所有子串的公共前缀。

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        int minLen = Integer.MAX_VALUE;
        for (String str : strs) {
            minLen = Math.min(minLen, str.length());
        }
        int low = 1;
        int high = minLen;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (isCommonPrefix(strs, mid))
                low = mid + 1;
            else
                high = mid - 1;
        }
        return strs[0].substring(0, (low + high) / 2);
    }
    private boolean isCommonPrefix(String[] strs, int Len) {
        String str1 = strs[0].substring(0, Len);
        for (int i = 1; i < strs.length; i++) {
            if (!strs[i].startsWith(str1)) {
                return false;
            }
        }
        return true;
    }
}
```
