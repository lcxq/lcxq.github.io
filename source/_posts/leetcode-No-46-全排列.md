---
title: leetcode No.46 全排列
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-18 16:45:01
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 全排列

给定一个**没有重复**数字的序列，返回其所有可能的全排列。

示例:

    输入: [1,2,3]
    输出:
    [
    [1,2,3],
    [1,3,2],
    [2,1,3],
    [2,3,1],
    [3,1,2],
    [3,2,1]
    ]

## 方法一

做得多了发现很多题思路都能相通，在No.31下一个排列的基础上修改一下即可。

先将给的数组排序，假设其长度为N，则对其操作N！次下一个排列即可。

PS.能AC的屎山也是好屎山

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        Arrays.sort(nums);
        if (nums.length == 0) {
            return res;
        }
        //这里用了流处理技巧将int数组转化为Integer型ArrayList,直接转换会因为泛型不匹配而报错
        res.add(Arrays.stream( nums ).boxed().collect(Collectors.toList()));
        int count = 1;
        int allNum = 1;
        //计算一下全排列数
        for (int i = 1; i <= nums.length; i++) {
            allNum *= i;
        }
        while (count++ < allNum) {
            nextPermutation(nums);
            res.add(Arrays.stream( nums ).boxed().collect(Collectors.toList()));
        }
        return res;
    }
    //以下代码直接拿No.31的轮子用
    public void nextPermutation(int[] nums) {
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }
        if (i == -1) {
            reverse(nums, 0);
            return;
        }
        int j = nums.length - 1;
        while (j > i && nums[j] <= nums[i]) {
            j--;
        }
        swap(nums, i, j);
        reverse(nums, i + 1);
    }
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    private void reverse(int[] nums, int i) {
        int j = nums.length - 1;
        while (i < j) {
            swap(nums, i++, j--);
        }
    }
}
```

## 方法二

标准的回溯法（DFS）

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        dfs(nums, new ArrayList<>());
        return res;
    }
    private void dfs(int[] nums, List<Integer> tempList) {
        if (tempList.size() == nums.length) {
            res.add(new ArrayList<>(tempList));
            return;
        } else {
            for (int i = 0; i < nums.length; i++) {
                if (tempList.contains(nums[i])) {
                    continue;
                }
                tempList.add(nums[i]);
                dfs(nums, tempList);
                tempList.remove(tempList.size() - 1);
            }
        }
    }
}
```

## 方法三

