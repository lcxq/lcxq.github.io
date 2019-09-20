---
title: leetcode No.43 字符串相乘
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-17 14:11:49
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 字符串相乘

给定两个以字符串形式表示的非负整数 *num1* 和 *num2*，返回 *num1* 和 *num2* 的乘积，它们的乘积也表示为字符串形式。

**示例 1:**

```markdown
输入: num1 = "2", num2 = "3"
输出: "6"
```

**示例 2:**

```markdown
输入: num1 = "123", num2 = "456"
输出: "56088"
```

**说明：**

1、num1 和 num2 的长度小于110。

2、num1 和 num2 只包含数字 0-9。

3、num1 和 num2 均不以零开头，除非是数字 0 本身。

4、**不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。**

## 方法一

大数相乘，自己按照竖式运算规则写了一个屎山居然AC了。

```java
class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) {
            return "0";
        }
        int[] num1List = new int[num1.length()];
        int[] num2List = new int[num2.length()];
        for (int i = num1.length() - 1, j = 0; i >= 0; i--, j++) {
            num1List[i] = Character.getNumericValue(num1.charAt(j));
        }
        for (int i = num2.length() - 1, j = 0; i >= 0; i--, j++) {
            num2List[i] = Character.getNumericValue(num2.charAt(j));
        }
        List<List<Integer>> res = new ArrayList<>();
        for (int i = 0; i < num2List.length; i++) {
            res.add(new ArrayList<>());
            for (int count_zero = 0; count_zero < i; count_zero++) {
                res.get(i).add(0);
            }
            int carry = 0;
            int num = num2List[i];
            int j = 0;
            while (j < num1List.length || carry != 0) {
                carry += num * (j < num1List.length ? num1List[j] : 0);
                ++j;
                res.get(i).add(carry % 10);
                carry /= 10;
            }
        }
        List<Integer> result = res.get(0);
        for (int i = 1; i < res.size(); i++) {
            result = BigInteger_add(result, res.get(i));
        }
        StringBuilder resultNum = new StringBuilder();
        for (int i = result.size() - 1; i >= 0; i--) {
            resultNum.append((char)(result.get(i) + '0'));
        }
        return resultNum.toString();
    }
    private List<Integer> BigInteger_add(List<Integer> num1, List<Integer> num2) {
        List<Integer> res = new ArrayList<>();
        int carry = 0;
        int i = 0, j = 0;
        while(i < num1.size() || j < num2.size() || carry != 0) {
            int m = (i < num1.size()) ? num1.get(i) : 0;
            int n = (j < num2.size()) ? num2.get(j) : 0;
            ++i;++j;
            carry += m + n;
            res.add(carry % 10);
            carry /= 10;
        }
        return res;
    }
}
```

## 方法二

观察发现，num1中第i位于num2中第j位相乘的结果一定放在答案的i+j位于i+j+1位。根据这个规律遍历两个数字字符串即可。

```java
class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) {
            return "0";
        }
        int n1 = num1.length();
        int n2 = num2.length();
        int[] pos = new int[n1 + n2]; //保存最后的结果
        for (int i = n1 - 1; i >= 0; i--) {
            for (int j = n2 - 1; j >= 0; j--) {
                int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                int sum = mul + pos[i + j + 1];
                pos[i + j] += sum / 10;
                pos[i + j + 1] = sum % 10;
            }
        }
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < pos.length; i++) {
            if (i == 0 && pos[i] == 0) {
                continue;
            }
            sb.append(pos[i]);
        }
        return sb.toString();
    }
}
```
