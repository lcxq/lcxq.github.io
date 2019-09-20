---
title: leetcode No.38 报数
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-12 12:19:26
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 报数

报数序列是一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

1.     1
2.     11
3.     21
4.     1211
5.     111221

1 被读作  "one 1"  ("一个一") , 即 11。

11 被读作 "two 1s" ("两个一"）, 即 21。

21 被读作 "one 2",  "one 1" （"一个二" ,  "一个一") , 即 1211。

给定一个正整数 n（1 ≤ n ≤ 30），输出报数序列的第 n 项。

注意：整数顺序将表示为一个字符串。

**示例 1:**

```markdown
输入: 1
输出: "1"
```

**示例 2:**

```markdown
输入: 4
输出: "1211"
```

## 方法

经典递归实现

```java
class Solution {
    public String countAndSay(int n) {
        return solver(n);
    }
    private String solver(int n) {
        if (n == 1) {
            return "1";
        } else {
            String cur = solver(n - 1);
            StringBuilder res = new StringBuilder();
            HashMap<Character, Integer> map = new HashMap<>();
            for (int i = 0; i < cur.length(); ++i) {
                char c = cur.charAt(i);
                if (map.containsKey(c)) {
                    map.put(c, map.get(c) + 1);
                } else {
                    if (!map.isEmpty()) {
                        res.append(String.valueOf(map.get(cur.charAt(i - 1))) + cur.charAt(i - 1));
                        map.clear();
                    }
                    map.put(c, 1);
                }
            }
            int lastIdx = cur.length() - 1;
            res.append(String.valueOf(map.get(cur.charAt(lastIdx))) + cur.charAt(lastIdx));
            return res.toString();
        }
    }
}
```

