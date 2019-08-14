---
title: leetcode No.1 两数之和
date: 2019-08-12 23:08:08
author: 硫茶小七
mathjax: true
categories: leetcode
top: false
cover: true
tags:
 - leetcode
 - 算法
 - Java
---

# 两数之和
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 方法一
无脑暴力就完事了，双重循环安排上
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] == target - nums[i]) {
                    return new int[] { i, j };
                }
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```
**时间复杂度：** $$O(n^2)$$

## 方法二
维护一个哈希表，实现数字到索引下标的映射，遍历数组时查询目标数字是否存在于表中
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target-nums[i]), i};
            }
            map.put(nums[i], i);
        }
        return new int[2];
    }
}
```
**时间复杂度：** $$O(n)$$