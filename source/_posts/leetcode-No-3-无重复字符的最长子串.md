---
title: leetcode No.3 无重复字符的最长子串
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-14 00:14:18
password:
summary:
tags: 
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 无重复字符的最长子串

给定一个字符串，请你找出其中不含有重复字符的**最长子串**的长度。

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 3:**
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

## 方法
滑动窗口法，维护 *i* 和 *j* 变量，分别指向窗口的头与尾。同时使用一个哈希表实现字符串中字符与下标的映射。

用变量 *j* (窗口尾端)遍历整个字符串，若表中已经存在该字符，说明当前的窗口可能已经出现了重复字符。此时将 *i* 前滑至该重复字符的后一位(直接从表中读取下标加**1**)，或是表中存在字符但窗口中不存在该字符，则 *i* 不变。用一行代码即可实现

`i = Math.max(map.get(s.charAt(j)) + 1, i);`

*i* 可以往前滑则往前滑，但不可以后退。

每次遍历都维护一下表，并维护一下窗口的最大长度。

最后返回遍历过程中最大的窗口长度即可。

```python
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int max_length = 0;
        HashMap<Character, Integer> map = new HashMap<>();
        for (int i = 0, j = 0; j < s.length(); j++) {
            if(map.containsKey(s.charAt(j))){
                i = Math.max(map.get(s.charAt(j)) + 1, i);
            }
            max_length = Math.max(max_length, j-i+1);
            map.put(s.charAt(j), j);
        }
        return max_length;
    }
}
```
**时间复杂度：** $$O(n)$$