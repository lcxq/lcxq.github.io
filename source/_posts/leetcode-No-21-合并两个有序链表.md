---
title: leetcode No.21 合并两个有序链表
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-28 12:54:49
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 合并两个有序链表

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

```markdown
示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

## 方法

数据结构链表基本题，很简单，直接贴代码。

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0);
        ListNode p = head;
        while (l1 != null && l2 != null) {
            if (l1.val > l2.val) {
                p.next = new ListNode(l2.val);
                l2 = l2.next;
            } else {
                p.next = new ListNode(l1.val);
                l1 = l1.next;
            }
            p = p.next;
        }
        if (l1 != null) {
            p.next = l1;
        }
        if (l2 != null) {
            p.next = l2;
        }
        return head.next;
    }
}
```
