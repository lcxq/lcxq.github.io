---
title: leetcode No.15 三数之和
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-24 15:04:09
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 三数之和

给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

```markdown
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## 方法一

暴力法直接TLE，这里用优化后的算法

大致思路是遍历数组，用零减去当前数字得到另外两个数字需要得到的和，再用头尾指针对撞搜索这两个数字。遍历过程中跳过重复出现的数字即可。

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums); //先将输入的数组排序
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        for (int i = 0; i < nums.length - 2; i++) {         //i遍历数组，头尾指针搜索i+1~nums.len-1，所以最后遍历到倒数第三个数字就行
            if (i == 0 || (i > 0 && nums[i] != nums[i - 1])) {  //遇到重复的数字跳过，不重复的数字才进行搜索
                int low = i + 1, high = nums.length - 1, sum = 0 - nums[i];
                while (low < high) {
                    if(nums[low] + nums[high] == sum){
                        res.add(Arrays.asList(nums[i], nums[low], nums[high]));
                        while(low < high && nums[low] == nums[low + 1]) low ++;
                        while(low < high && nums[high] == nums[high - 1]) high --;
                        low ++;
                        high --;
                    }else if(nums[low] + nums[high] < sum) low ++;
                    else high--;
                }
            }
        }
        return res;
    }
}
```

**时间复杂度：** $$O(n^2)$$
