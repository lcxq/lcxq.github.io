---
title: leetcode No.45 跳跃游戏Ⅱ
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-18 12:59:25
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 跳跃游戏Ⅱ

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

**示例:**

    输入: [2,3,1,1,4]
    输出: 2
    解释: 跳到最后一个位置的最小跳跃数是 2。
        从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。

**说明:**

假设你总是可以到达数组的最后一个位置。

## 方法一

看了tag的贪心算法就自己AC了......

遍历当前可以到达的位置，在可达位置的基础上加上跳跃距离就是再下一个可达位置。以该位置最大为搜索目标。

```java
class Solution {
    public int jump(int[] nums) {
        if (nums.length == 1) {
            return 0;
        }
        int here_index = 0, count = 0;
        while (here_index < nums.length) {
            int next_index = 0;
            int max = 0;
            for (int i = here_index + 1; i <= here_index + nums[here_index]; i++) {
                if (i >= nums.length - 1) {
                    count++;
                    return count;
                } else {
                    int prob_index = nums[i] + i;
                    if (prob_index > max) {
                        max = prob_index;
                        next_index = i;
                    }
                }
            }
            here_index = next_index;
            count ++;
        }
        return count;
    }
}
```

## 方法二

其实是同样的思路，代码简洁了不少，运行时间也少了。

```java
class Solution {
    public int jump(int[] nums) {
        int end = 0;
        int maxPosition = 0; 
        int steps = 0;
        for(int i = 0; i < nums.length - 1; i++){
            //找能跳的最远的
            maxPosition = Math.max(maxPosition, nums[i] + i); 
            if(i == end){ //遇到边界，就更新边界，并且步数加一
                end = maxPosition;
                steps++;
            }
        }
        return steps;
    }
}
```
