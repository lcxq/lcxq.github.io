---
title: leetcode No.42 接雨水
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-17 13:56:10
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 接雨水

给定 *n* 个非负整数表示每个宽度为 **1** 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

![接雨水示意图](https://s2.ax1x.com/2019/09/17/n5EqS0.png)

上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 感谢 Marcos 贡献此图。

**示例:**

```markdown
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```

第一眼没啥思路，看了看大佬的解答

这道题的关键在于按列求算水的量。当前列水的量由当前列左侧所有列的最大值与右侧所有列的最大值两者的较小值决定。同时，只有当该值大于当前列的高度才会有水。

总结一下步骤：

    1、遍历所有列，假设当前列为*i*列。
    2、分别找出 0 ~ i - 1 与 i + 1 ~ height.length - 1 的最大值max_left与max_right。
    3、比较max_left与max_right，保留较小者为min。
    4、比较min与当前列高度，如果min大于当前列高度则累加水的体积。水的体积为min减去当前列高度。

```java
//用双指针法从左右两端移动可以减小空间复杂度
class Solution {
    public int trap(int[] height) {
        int max_left = 0, max_right = 0;
        int left = 1, right = height.length - 2;
        int sum = 0;
        while (left <= right) {
            if (height[left - 1] < height[right + 1]) {
                max_left = Math.max(max_left, height[left - 1]);
                if (max_left > height[left]){
                    sum += (max_left - height[left]);
                }
                left ++;
            } else {
                max_right = Math.max(max_right, height[right + 1]);
                if (max_right > height[right]) {
                    sum += (max_right - height[right]);
                }
                right --;
            }
        }
        return sum;
    }
}
```
