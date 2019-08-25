---
title: leetcode No.17 电话号码的字母组合
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-25 13:59:31
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 电话号码的字母组合

![](https://s2.ax1x.com/2019/08/25/mgMuAe.png)

## 方法一

递归实现，DFS的思路

```java
class Solution {
    List<String> res = new ArrayList<>();
    String[] map = new String[]{"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    public List<String> letterCombinations(String digits) {
        if(digits.isEmpty()) return new ArrayList<String>();
        deal(digits, 0, "");
        return res;
    }
    private void deal(String digits, int index, String tempStr) {
        if(index == digits.length()){
            res.add(tempStr);
        }else{
            int num = digits.charAt(index) - '0';
            String str = map[num];
            for (int i = 0; i < str.length(); i++) {
                deal(digits, index + 1, tempStr + str.charAt(i));
            }
        }
    }
}
```

## 方法二

迭代实现，使用队列。先将第一个数字对应的字母全部入队，再分别出队，出队时将出队字母与下一个数字所对应的字母合并再入队。所有的数字全部遍历完毕后得到的队列就是答案。

```java
class Solution {
    String[] map = new String[]{"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    public List<String> letterCombinations(String digits) {
        if(digits.isEmpty()) return new ArrayList<String>();
        LinkedList<String> que = new LinkedList<String>();
        que.add("");
        for (int i = 0; i < digits.length(); i++) {
            int num = Character.getNumericValue(digits.charAt(i));
            while (que.peek().length() == i) {
                String temp = que.remove();
                for (char s : map[num].toCharArray()) {
                    que.add(temp + s);
                }
            }
        }
        return que;
    }
}
```
