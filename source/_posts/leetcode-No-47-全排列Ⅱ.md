---
title: leetcode No.47 全排列Ⅱ
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-20 12:14:55
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 全排列Ⅱ

给定一个可包含重复数字的序列，返回所有不重复的全排列。

**示例:**

    输入: [1,1,2]
    输出:
    [
    [1,1,2],
    [1,2,1],
    [2,1,1]
    ]

## 方法

在上一题的回溯基础上进行修改

    1、因为存在重复的数组所以需要修改上一题中直接判断当前tempList中是否包含当前数字的方法，改为设置一个used数组记录当前索引的这个数字是否使用过。
    2、加一个新的剪枝条件 (i>0 && nums[i] == nums[i - 1] && !used[i - 1]) 意思是当前数字和之前的数字相同而且前一个相同的数字还在待选集合没有使用过时，剪枝

```java
 class Solution {
    List<List<Integer>> res = new ArrayList<>();
    boolean[] used;
    public List<List<Integer>> permuteUnique(int[] nums) {
        if (nums.length == 0) {
            return res;
        }
        //记得排序，将重复数字放在一起便于去重
        Arrays.sort(nums);
        used = new boolean[nums.length];
        dfs(new Stack<>(), nums);
        return res;
    }
    private void dfs(Stack<Integer> tempList, int[] nums) {
        if (tempList.size() == nums.length) {
            res.add(new ArrayList<>(tempList));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (!used[i]) {
                if (i != 0 && nums[i] == nums[i - 1] && !used[i - 1]) {
                    continue;
                }
                used[i] = true;
                tempList.add(nums[i]);
                dfs(tempList, nums);
                tempList.pop();
                used[i] = false;
            }
        }
    }
}
```
