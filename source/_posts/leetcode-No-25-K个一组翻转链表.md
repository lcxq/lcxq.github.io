---
title: leetcode No.25 K个一组翻转链表
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-01 13:20:29
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# K个一组翻转链表

又一道自己AC的Hard题，开心。

## 方法

链表题难度还是不大的。这个题可以拆分成两个部分，一个是从链表中抽出K长度的子链表，一个是翻转链表。

翻转链表是数据结构的必学题，这里用头插法实现翻转。K个一组就从开始先遍历K步记录子链表的结尾即可，剩下的就是细节的实现了。

顺便解释一下各个指针的含义，以1，2，3，4，5，6，7这个链表为例，K=3

首先自己新建头结点方便操作，用Head标记。

ptrHead表示每个待翻转的子链表的前一个节点。例子中1，2，3子链表的ptrHead是Head, 4,5,6子链表的ptrHead是3结点。

ptrEnd标记子链表的最后一个结点，例如1，2，3子链表的ptrEnd是3结点。

ptrlow标记子链表的第一个结点，例如1，2，3子链表的ptrlow是1结点。由于ptrlow指向的节点经过翻转后会变为子链表的最后一个节点，所以它的next指针需要指向下一个子链表的开头。

ptr标记当前需要进行头插操作的节点，会在遍历子链表的过程中不断推进。

ptrNextLow标记下一个子链表的开头。因此翻转链表操作结束后ptrlow的next需要连接该节点。例如1，2，3子链表的

ptrLate标记当前节点即ptr节点的下一个节点，用于防止当前节点的next链接的改变而丢失后续链表。

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || k == 1) {
            return head;
        }
        ListNode Head = new ListNode(0);
        Head.next = head;
        ListNode ptrHead = Head, ptrEnd = Head;
        while (true) {
            ptrEnd = ptrHead;
            int count = 0;
            for (int i = 0; i < k; i++) {
                if (ptrEnd.next != null) {
                    ptrEnd = ptrEnd.next;
                    count ++;
                }
            }
            if (count < k) break;
            ListNode ptrlow = ptrHead.next, ptr = ptrlow.next, ptrNextLow = ptrEnd.next;
            while (ptr != ptrNextLow) {
                ListNode ptrLate = ptr.next;
                ptr.next = ptrHead.next;
                ptrHead.next = ptr;
                ptr = ptrLate;
            }
            ptrlow.next = ptrNextLow;
            ptrHead = ptrlow;
        }
        return Head.next;
    }
}
```
