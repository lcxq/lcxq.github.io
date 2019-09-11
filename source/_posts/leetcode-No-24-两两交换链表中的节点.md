---
title: leetcode No.24 两两交换链表中的节点
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-31 15:24:47
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 两两交换链表中的节点

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例:

```markdown
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

## 方法一

链表题画个图差不多就能理清楚怎么调整节点指针了。先用迭代实现。

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0); 
        dummy.next = head;
        ListNode point = dummy;
        while (point.next != null && point.next.next != null) {
            ListNode swap1 = point.next, swap2 = point.next.next;
            point.next = swap2;
            swap1.next = swap2.next;
            swap2.next = swap1;
            point = swap1;
        }
        return dummy.next;
    }
}
```

## 方法二

递归实现

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode n = head.next;
        head.next = swapPairs(head.next.next);
        n.next = head;
        return n;
    }
}
```
