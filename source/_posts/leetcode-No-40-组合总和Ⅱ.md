---
title: leetcode No.40 组合总和Ⅱ
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-15 23:57:14
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 组合总和Ⅱ

给定一个数组 *candidates* 和一个目标数 *target* ，找出 *candidates* 中所有可以使数字和为 *target* 的组合。

*candidates* 中的每个数字在每个组合中只能使用一次。

**说明：**

    所有数字（包括目标数）都是正整数。

    解集不能包含重复的组合。

**示例 1:**

```markdown
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**示例 2:**

```markdown
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```

## 方法

在上一题的基础上加一个防止重复的步骤以及由于每个数字仅用一次，所以搜索完当前数字就直接看下一个数字。在搜索之前对数组排序便于免重复。

```java
class Solution {
    HashMap<Integer, Integer> allResults = new HashMap<>();
    List<List<Integer>> res = new ArrayList<>();
    int[] nums;
    int target;
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        this.nums = candidates;
        this.target = target;
        Arrays.sort(nums);
        dfs(new ArrayList<>(), 0, target);
        return res;
    }
    private void dfs(List<Integer> tempList, int start, int remain) {
        if (remain < 0) {
            return;
        } else if (remain == 0) {
            int number = 0;
            for (int i = 0; i < tempList.size(); i++) {
                number = number * 10 + tempList.get(i);
            }
            if (allResults.containsKey(number)) {
                return;
            } else {
                res.add(new ArrayList<>(tempList));
                allResults.put(number, 1);
            }
        } else {
            for (int i = start; i < nums.length; i++) {
                tempList.add(nums[i]);
                dfs(tempList, i + 1, remain - nums[i]);
                tempList.remove(tempList.size() - 1);
            }
        }
    }
}
```
