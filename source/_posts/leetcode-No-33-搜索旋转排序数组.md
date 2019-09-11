---
title: leetcode No.33 搜索旋转排序数组
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-10 14:44:31
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 搜索旋转排序数组

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

**示例 1:**

```markdown
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```

**示例 2:**

```markdown
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```

## 方法

先二分查找搜索出旋转点，即数组的最小值，可以将数组分为升序的两段，且前段最小值大于后段最大值。再根据前段最小值与target大小比较结果在某一段中二分查找目标数字。

```java
class Solution {
    int[] nums;
    int target;
    private int find_rotate_index(int left, int right) {
        if (nums[left] < nums[right]) {
            return 0;
        }
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] > nums[mid + 1]) {
                return mid + 1;
            } else {
                if (nums[left] > nums[mid]) {
                    right = mid - 1;
                } else left = mid + 1;
            }
        }
        return 0;
    }
    private int search(int left, int right) {
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] == target) {
                return mid;
            } else {
                if (nums[mid] > target) {
                    right = mid - 1;
                } else left = mid + 1;
            }
        }
        return -1;
    }
    public int search(int[] nums, int target) {
        this.nums = nums;
        this.target = target;
        int n = nums.length;
        if (n == 0) return -1;
        if (n == 1) return (nums[0] == target ? 0 : -1);
        int rotate_index = find_rotate_index(0, n - 1);
        if (rotate_index == 0) {
            return search(0, n - 1);
        }
        if (nums[0] > target) {
            return search(rotate_index, n - 1);
        } else {
            return search(0, rotate_index - 1);
        }
    }
}
```
