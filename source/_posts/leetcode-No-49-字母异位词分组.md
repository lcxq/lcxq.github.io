---
title: leetcode No.49 字母异位词分组
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-20 14:50:36
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 字母异位词分组

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

**示例:**

    输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
    输出:
    [
    ["ate","eat","tea"],
    ["nat","tan"],
    ["bat"]
    ]

**说明：**

    所有输入均为小写字母。
    不考虑答案输出的顺序。

## 方法

自己想到的方法，但实现出了点小问题，参考了一下答案。

思路很简单，遍历字符串数组，对当前字符串按字典序排序。借助一个HashMap实现分组。

自己实现过程时是将HashMap实现String与该Str所在list的索引的映射。但发现无法实现在二维list中添加元素的操作。答案是直接将HashMap实现String与List< String>的映射，返回答案时将HashMap的value创建List< List< String >>。

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> hash = new HashMap<>();
        for (int i = 0; i < strs.length; i++) {
            char[] s_arr = strs[i].toCharArray();
            Arrays.sort(s_arr);
            String key = String.valueOf(s_arr);
            if (hash.containsKey(key)) {
                hash.get(key).add(strs[i]);
            } else {
                List<String> temp = new ArrayList<String>();
                temp.add(strs[i]);
                hash.put(key, temp);
            }
        }
        return new ArrayList<List<String>>(hash.values());
    }
}
```
