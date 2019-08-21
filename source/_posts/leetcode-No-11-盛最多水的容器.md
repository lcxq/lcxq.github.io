---
title: leetcode No.11 盛最多水的容器
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-22 00:24:58
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 盛最多水的容器

![题目描述](https://s2.ax1x.com/2019/08/22/ma3Zss.png)

## 方法

最简单的两层循环暴力法就不写了，这里直接贴上官方题解的双指针解法。

大致思路就是，设置 *i , j* 两个指针分别从头尾向中间靠拢。由于最大容积仅由较短边决定，因此每次迭代让较短的一边的指针往中间移动，同时维护最大容积的值。

```java
class Solution {
    public int maxArea(int[] height) {
        int maxV = 0, r = 0, l = height.length - 1;
        while(r < l) {
            maxV = Math.max(Math.min(height[r], height[l]) * (l - r), maxV);
            if(height[r] > height[l]){
                l--;
            }else{
                r++;
            }
        }
        return maxV;
    }
}
```

**时间复杂度：** $$O(n)$$
