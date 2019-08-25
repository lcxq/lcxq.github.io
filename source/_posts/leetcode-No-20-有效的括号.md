---
title: leetcode No.20 有效的括号
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-26 00:37:37
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

**示例 1:**

```markdown
输入: "()"
输出: true
```

**示例 2:**

```markdown
输入: "()[]{}"
输出: true
```

**示例 3:**

```markdown
输入: "(]"
输出: false
```

**示例 4:**

```markdown
输入: "([)]"
输出: false
```

**示例 5:**

```markdown
输入: "{[]}"
输出: true
```

## 方法

学栈的时候就见过的题，用栈实现即可，把各种情况罗列一下。

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack<>();
        for (char c : s.toCharArray()) {
            if ((c == ')' || c == ']' || c == '}') && st.empty()) {
                return false;
            }else if((c == ')' || c == ']' || c == '}')){
                if(c == ')' && st.peek() == '('){
                    st.pop();
                }else if(c == ')' && st.peek() != '(') return false;
                if(c == ']' && st.peek() == '['){
                    st.pop();
                }else if(c == ']' && st.peek() != '[') return false;
                if(c == '}' && st.peek() == '{'){
                    st.pop();
                }else if(c == '}' && st.peek() != '{') return false;
            }else if(c == '(' || c == '[' || c == '{')
                st.push(c);
            }
        if(st.empty()) return true;
        else return false;
    }
}
```
