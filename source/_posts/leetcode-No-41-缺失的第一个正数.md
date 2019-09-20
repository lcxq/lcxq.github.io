---
title: leetcode No.41 缺失的第一个正数
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-16 12:17:10
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 缺失的第一个正数

给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

**示例 1:**

```markdown
输入: [1,2,0]
输出: 3
```

**示例 2:**

```markdown
输入: [3,4,-1,1]
输出: 2
```

**示例 3:**

```markdown
输入: [7,8,9,11,12]
输出: 1
```

**说明:**

你的算法的时间复杂度应为O(n)，并且只能使用常数级别的空间。

## 方法

直接参考别人的解法了。

解法主要有两个要点：

1、将遍历过程中遇到的正整数放到数组的对应索引的位置。例如遇1就放到0号位（第一个位置），遇到3就放到2号位（第三个位置）。遇到非正整数或者大于数组长度的数就无视（大于数组长度的数之前一定会有答案）。

2、利用交换的方法节省空间

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            while (nums[i] > 0 && nums[i] <= nums.length && nums[i] != nums[nums[i] - 1]) {
                swap(nums, i, nums[i] - 1);
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }
        return nums.length + 1;
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```
