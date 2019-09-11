---
title: leetcode No.31 下一个排列
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-06 17:03:07
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 下一个排列

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须原地修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1

## 方法

没啥很好的思路，直接看题解了。

这题关键在于分析，分析出来之后就比较简单了，要获取下一个排列步骤如下：

1. 从后向前遍历，找到第一个出现的i元素使得nums[ i ] < nums[i - 1]

2. 找出i ~ nums.length - 1 元素中大于nums[ i ]中最小的那一个nums[ j ]

3. 交换 i 与 j

4. 翻转 j + 1 ~ nums.length - 1

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        //找到第一个不再递增的位置
        while (i >= 0 && nums[i + 1] <= nums[i]) {
            i--;
        }
        //如果到了最左边，就直接倒置输出
        if (i < 0) {
            reverse(nums, 0);
            return;
        }
        //找到刚好大于 nums[i]的位置
        int j = nums.length - 1;
        while (j >= 0 && nums[j] <= nums[i]) {
            j--;
        }
        //交换
        swap(nums, i, j);
        //利用倒置进行排序
        reverse(nums, i + 1);
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[j];
        nums[j] = nums[i];
        nums[i] = temp;
    }
    private void reverse(int[] nums, int start) {
        int i = start, j = nums.length - 1;
        while (i < j) swap(nums, i ++, j ++);
    }
}
```
