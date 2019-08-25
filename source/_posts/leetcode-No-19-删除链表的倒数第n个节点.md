---
title: leetcode No.19 删除链表的倒数第n个节点
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-25 22:58:27
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 删除链表的倒数第n个节点

给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

```markdown
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 n 保证是有效的。

**进阶：**

你能尝试使用一趟扫描实现吗？

## 方法

链表倒数某个节点的题基本都是快慢指针做，删除节点的话标记一下前一个节点就行。

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode p1 = new ListNode(0);
        ListNode p2 = new ListNode(0);
        p2 = head;
        p1.next = head;
        for (int i = 0; i < n; i++) {
            p2 = p2.next;
        }
        while(p2 != null){
            p1 = p1.next;
            p2 = p2.next;
        }
        if(p1.next == head){
            return head.next;
        }else{
            p1.next = p1.next.next;
            return head;
        }
    }
}
```

**时间复杂度：** $$O(n)$$
