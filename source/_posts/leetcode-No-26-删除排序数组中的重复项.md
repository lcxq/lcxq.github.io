---
title: leetcode No.26 删除排序数组中的重复项
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-02 18:57:33
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 删除排序数组中的重复项

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

**示例 1:**

```markdown
给定数组 nums = [1,1,2],

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。

你不需要考虑数组中超出新长度后面的元素。
```

**示例 2:**

```markdown
给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
```

## 方法

很简单的题，直接贴代码

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int ptr = 0, i = 0;
        while (i < nums.length) {
            nums[ptr++] = nums[i++];
            while (i < nums.length && nums[i] == nums[i - 1]) {
                ++i;
            }
        }
        return ptr;
    }
}
```
