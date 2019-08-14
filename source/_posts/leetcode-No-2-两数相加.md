---
title: leetcode No.2 两数相加
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-12 23:47:19
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---
# 两数相加
给出两个**非空**的链表用来表示两个非负的整数。其中，它们各自的位数是按照**逆序**的方式存储的，并且它们的每个节点只能存储__一位__数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例：**
```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

## 方法
基本的链表操作+高精度求和运算，用一个carry变量记录求和结果即可
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int carry = 0;
        ListNode p,head = new ListNode(0);
        head.next = null;
        p = head;
        while (l1!=null ||l2!=null||carry!=0) {
            if (l1!=null) {
                carry += l1.val;
                l1 = l1.next;
            }
            if (l2!=null) {
                carry += l2.val;
                l2 = l2.next;
            }
            p.next = new ListNode(carry%10);
            carry /=10;
            p = p.next;
        }
        return head.next;
    }
}
```