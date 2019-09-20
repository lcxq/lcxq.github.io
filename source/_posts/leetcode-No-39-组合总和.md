---
title: leetcode No.39 组合总和
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-15 22:54:23
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 组合总和

**说明：**

    所有数字（包括 target）都是正整数。

    解集不能包含重复的组合。

**示例 1:**

```markdown
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
```

**示例 2:**

```markdown
输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

## 方法

回溯法，也可以看成dfs

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        dfs(res, new ArrayList<>(), 0, target, candidates);
        return res;
    }
    private void dfs(List<List<Integer>> res, List<Integer> tempList, int start, int remain, int[] nums) {
        if (remain < 0) {
            return;
        } else if (remain == 0) {
            res.add(new ArrayList<>(tempList));
            return;
        } else {
            for (int i = start; i < nums.length; i++) {
                tempList.add(nums[i]);
                dfs(res, tempList, i, remain - nums[i], nums);
                tempList.remove(tempList.size() - 1);
            }
        }
    }
```
