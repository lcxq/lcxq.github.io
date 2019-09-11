---
title: leetcode No.34 在排序数组中查找元素的第一个和最后一个位置
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-10 19:35:35
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 在排序数组中查找元素的第一个和最后一个位置

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 [-1, -1]。

**示例 1:**

```markdown
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```

**示例 2:**

```markdown
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

## 方法

先二分找目标数字，找到后将目标数字视为分割点将数组分为前后两段，再分别二分查找区间起始和终点位置。

```java
class Solution {
    int[] nums;
    int target;
    public int[] searchRange(int[] nums, int target) {
        this.nums = nums;
        this.target = target;
        if (nums.length == 0) {
            return new int[]{-1,-1};
        }
        if (nums.length == 1) {
            if (nums[0] == target) {
                return new int[]{0,0};
            } else return new int[]{-1,-1};
        }
        int mid = search(0, nums.length - 1);
        if (mid == -1) {
            return new int[]{-1,-1};
        }
        int left = search_low_boundary(mid);
        int right = search_high_boundary(mid);
        return new int[]{left, right};
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
    private int search_low_boundary(int high) {
        int left = 0, right = high;
        if (nums[left] == target) {
            return left;
        }
        while (left <= right) {
            int mid = (left + right) / 2;
            if (mid + 1 < nums.length && nums[mid] != target && nums[mid + 1] == target) {
                return mid + 1;
            } else if (mid - 1 >= 0 && nums[mid] == target && nums[mid - 1] != target) {
                return mid;
            } else {
                if (nums[mid] == target) {
                    right = mid -1;
                } else {
                    left = mid + 1;
                }
            }
        }
        return -1;
    }
    private int search_high_boundary(int low) {
        int left = low, right = nums.length - 1;
        if (nums[right] == target) {
            return right;
        }
        while (left <= right) {
            int mid = (left + right) / 2;
            if (mid + 1 < nums.length && nums[mid] == target && nums[mid + 1] != target) {
                return mid;
            } else if (mid - 1 >= 0 && nums[mid] != target && nums[mid - 1] == target) {
                return mid - 1;
            } else {
                if (nums[mid] != target) {
                    right = mid -1;
                } else {
                    left = mid + 1;
                }
            }
        }
        return -1;
    }
}
```

## 方法二

自己写的代码长到自己都看不过去了，看了下题解优化一下。设置一个left的布尔变量来分开执行左区间迭代和右区间迭代。

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = {-1, -1};
        int leftIdx = search(nums, target, true);
        if (leftIdx == nums.length || nums[leftIdx] != target) {
            return res;
        }
        res[0] = leftIdx;
        res[1] = search(nums, target, false) - 1;
        return res;
    }
    private int search(int[] nums, int target, boolean left) {
        int lo = 0, hi = nums.length;
        while (lo < hi) {
            int mid = (lo + hi) / 2;
            //解释一下left的作用
            //当left为false时，就是向右一直二分迭代直到找到大于target的最小数
            //当left为true时，分为几种情况
            //1、区间完全在左（右）段，则hi（lo）迭代向左（右）移动
            //2、当区间横跨了左右段时，hi迭代向左
            //最后的结果lo将会停在区段的左端点。
            if (nums[mid] > target || (left && nums[mid] == target)) {
                hi = mid;
            } else lo = mid + 1;
        }
        return lo;
    }
}
```

官方题解还是巧妙啊......
