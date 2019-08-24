---
title: leetcode No.16 最接近的三数之和
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-24 20:06:37
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 最接近的三数之和

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

```markdown
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

## 方法

首先暴力可解，这里只放优化后的方法。解法与上一题基本相同，即遍历数组同时用双指针搜索即可。

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int sub = Integer.MAX_VALUE;
        int res = 0;
        for (int i = 0; i < nums.length - 2; i++) {
            int low = i + 1, high = nums.length - 1;
            while(low < high){
                int sum = nums[low] + nums[high] + nums[i];
                int temp = Math.abs(sum - target);
                if(sum == target) return target;
                if (temp < sub) {
                    sub = temp;
                    res = sum;
                }
                if (sum > target) {
                    high --;
                } else {
                    low ++;
                }
            }
        }
        return res;
    }
}
```

**时间复杂度：** $$O(n^2)$$
