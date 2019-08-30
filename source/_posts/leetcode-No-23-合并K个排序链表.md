---
title: leetcode No.23 合并K个排序链表
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-30 14:36:49
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 合并K个排序链表

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:

```markdown
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

## 方法一

零参考自己AC的第一个hard题，开心。

方法很简单，在No.21合并两个有序链表的基础上套上分治模板，递归实现。

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) {
            return null;
        }
        ListNode head = RecursionMerge(lists, 0, lists.length - 1);
        return head;
    }
    private ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode head = new ListNode(0), p = head;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                p.next = l1;
                l1 = l1.next;
            } else {
                p.next = l2;
                l2 = l2.next;
            }
            p = p.next;
        }
        if (l1 != null) {
            p.next = l1;
        } else if (l2 != null) {
            p.next = l2;
        }
        return head.next;
    }
    private ListNode RecursionMerge(ListNode[] lists, int left, int right) {
        if (left == right) {
            return lists[left];
        } else if (right == left + 1){
            return mergeTwoLists(lists[left], lists[right]);
        } else {
            int mid = (left + right) / 2;
            ListNode l1 = RecursionMerge(lists, left, mid);
            ListNode l2 = RecursionMerge(lists, mid + 1, right);
            return mergeTwoLists(l1, l2);
        }
    }
}
```

## 方法二

最容易想到的方法，就是不断遍历所有的链表首节点寻找最小值加入答案链表。

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode head = new ListNode(0), p = head;
        while (true) {
            boolean allNull = true;
            int min = 0x3f3f3f3f;
            int min_index = 0;
            for (int i = 0; i < lists.length; i++) {
                if (lists[i] != null) {
                    allNull = false;
                    if (lists[i].val < min) {
                        min = lists[i].val;
                        min_index = i;
                    }
                }
            }
            if (allNull) break;
            p.next = lists[min_index];
            p = p.next;
            lists[min_index] = lists[min_index].next;
        }
        return head.next;
    }
}
```

## 方法三

使用优先队列可以自动实现选出值最小的节点（通过这个方法学习一下Java中优先队列的使用）

```java
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        //定义优先队列的比较器
        Comparator<ListNode> cmp;
        cmp = new Comparator<ListNode>() {
            public int compare(ListNode l1, ListNode l2) {
                return l1.val - l2.val;
            }
        };
        //建队列
        Queue<ListNode> q = new PriorityQueue<ListNode>(cmp);
        //所有链表的首节点先入队
        for (ListNode l : lists) {
            if (l != null) {
                q.add(l);
            }
        }
        ListNode head = new ListNode(0), point = head;
        while (!q.isEmpty()) {
            //出队列
            point.next = q.poll();
            point = point.next;
            ListNode next = point.next;
            if (next != null) {
                q.add(next);
            }
        }
        return head.next;
    }
}
```
