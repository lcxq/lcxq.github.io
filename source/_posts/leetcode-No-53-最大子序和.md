---
title: leetcode No.53 最大子序和
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-27 16:58:02
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

## 最大子序和

给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**示例:**

    输入: [-2,1,-3,4,-1,2,1,-5,4],
    输出: 6
    解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

**进阶:**

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

## 方法一

动态规划思路，遍历过程中不断判断当前位置数字和加和数字大小并记录最大值即可。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int dp = nums[0];
        int max = nums[0]; 
        for (int i = 1; i < n; i++) {
            dp = Math.max(dp + nums[i], nums[i]);
            max = Math.max(max, dp);
        }
        return max;
    }
}
```

**时间复杂度：** $$O(n)$$
**空间复杂度：** $$O(1)$$
