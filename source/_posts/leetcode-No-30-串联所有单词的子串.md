---
title: leetcode No.30 串联所有单词的子串
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-03 17:29:15
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 串联所有单词的子串

给定一个字符串 s 和一些长度相同的单词 words。找出 s 中恰好可以由 words 中所有单词串联形成的子串的起始位置。

注意子串要与 words 中的单词完全匹配，中间不能有其他字符，但不需要考虑 words 中单词串联的顺序。

**示例 1：**

```markdown
输入：
  s = "barfoothefoobarman",
  words = ["foo","bar"]
输出：[0,9]
解释：
从索引 0 和 9 开始的子串分别是 "barfoor" 和 "foobar" 。
输出的顺序不重要, [9,0] 也是有效答案。
```

**示例 2：**

```markdown
输入：
  s = "wordgoodgoodgoodbestword",
  words = ["word","good","best","word"]
输出：[]
```

## 方法一

没啥很好的解体思路，直接看别人的答案了。

首先确定遍历s串的子串判断是否匹配的方法。难点在于无需考虑顺序的话能够匹配的子串就有很多种可能。因此我们可以建立一个哈希表保存words中各个单词的数量。在遍历s串的过程中，子串也建立一个哈希表记录子串中单词出现的数目。如果两个哈希表中的单词与其数目均相同的话，则匹配成功。

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        List<Integer> res = new ArrayList<>();
        if (words.length == 0) {
            return res;
        }
        int wordLen = words[0].length();
        int wordNum = words.length;
        HashMap<String, Integer> allWords = new HashMap<>();
        for (String str : words) {
            int value = allWords.getOrDefault(str, 0);
            allWords.put(str, value + 1);
        }
        for (int i = 0; i < s.length() - wordLen * wordNum + 1; i++) {
            HashMap<String, Integer> hasWords = new HashMap<>();
            int num = 0;
            while (num < wordNum) {
            String word = s.substring(i + num * wordLen, i + (num + 1) * wordLen);
                if (allWords.containsKey(word)) {
                    int value = hasWords.getOrDefault(word, 0);
                    hasWords.put(word, value + 1);
                    if (hasWords.get(word) > allWords.get(word)) {
                        break;
                    }
                } else break;
                num ++;
            }
            if (num == wordNum) {
                res.add(i);
            }
        }
        return res;
    }
}
```

## 方法二

法二是在法一基础上的优化，代码有点复杂，先留坑。
