---
title: leetcode No.35 搜索插入位置
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-10 23:30:03
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

**示例 1:**

```markdown
输入: [1,3,5,6], 5
输出: 2
```

**示例 2:**

```markdown
输入: [1,3,5,6], 2
输出: 1
```

**示例 3:**

```markdown
输入: [1,3,5,6], 7
输出: 4
```

**示例 4:**

```markdown
输入: [1,3,5,6], 0
输出: 0
```

## 方法

二分，越写越熟了。[liweiwei1919](https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/)的二分法总结写的不错。

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums[0] > target) {
            return 0;
        }
        if (nums[nums.length - 1] < target) {
            return nums.length;
        }
        int low = 0, high = nums.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (nums[mid] == target) {
                return mid;
            } else {
                if (nums[mid] < target) {
                    low = mid + 1;
                } else high = mid - 1;
            }
        }
        return low;
    }
}
```
