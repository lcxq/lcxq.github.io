---
title: leetcode No.4 寻找两个有序数组的中位数
top: false
cover: true
toc: true
mathjax: true
date: 2019-08-16 00:09:27
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 寻找两个有序数组的中位数

给定两个大小为 m 和 n 的有序数组 **nums1** 和 **nums2**。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。

你可以假设 **nums1** 和 **nums2** 不会同时为空。

**示例 1:**

```markdown
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```

**示例 2:**

```markdown
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

第一道leetcode上遇到的hard题，难点在于满足log复杂度。题解研究了两天总算是看的差不多了，排除直接遍历或是合并有序数组的方法复杂度都在O(m+n)，也比较简单，就不写了。下面主要写两个解法。

## 方法一

**时间复杂度：** $$O(log(min(m,n)))$$

leetcode官方题解的思路，大致意思就是根据中位数的性质。  

1) 中位数能将所有数分为两个等大小的部分
2) 中位数一边的所有数字一定小于等于另一边

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if( nums1.length >nums2.length){
            int []temp = nums1;nums1 = nums2;nums2 = temp; //保证 i 遍历的一定是较短数组
        }
        int m = nums1.length, n = nums2.length;
        int iMax = m, iMin = 0;   //用于记录二分遍历的头尾
        int halfLen = (m+n+1)/2;  //用于计算 j
        while (iMin <= iMax) {
            int i = (iMax+iMin)/2;//二分法搜索 i
            int j = halfLen - i;  //用于根据 i 直接计算 j, 利用性质1)可以推出
            if(i!=m && j!=0 && nums2[j-1]>nums1[i]){  //找到的i太小了，要往大了找
                iMin = i + 1;
            }
            else if (i!=0 && j!=n && nums1[i-1]>nums2[j]) { //找到的i太大了，要往小了找
                iMax = i-1;
            } else {                                            //找到的i刚好满足中位数性质，并分类讨论边界情况返回答案
                int maxLeft = 0;                            //分析小于中位数的部分
                if(i==0){ maxLeft = nums2[j-1];}
                else if (j==0){ maxLeft = nums1[i-1];}
                else maxLeft = Math.max(nums1[i-1], nums2[j-1]);

                if(((m+n) % 2 == 1)) return maxLeft;        //总长奇数，直接返回左半边的最大值为中位数

                int minRight = 0;                           //分析大于中位数的部分
                if(i==m){ minRight = nums2[j];}
                else if(j==n){ minRight = nums1[i];}
                else minRight = Math.min(nums1[i], nums2[j]);

                return (maxLeft+minRight)/2.0;  //总厂偶数，返回左最大和右最小的平均数
            }
        }
        return 0.0;
    }
}
```

## 方法二

[windliang](https://leetcode-cn.com/problems/two-sum/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-w-2/)总结的方法

递归法，思路在于：找中位数就是找第k小的数，其中k=(m+n)/2，每次遍历就排除掉k/2个数即可

```java

class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;
        int left = (n + m + 1) / 2;
        int right = (n + m + 2) / 2;
        //将偶数和奇数的情况合并，如果是奇数，会求两次同样的 k 。
        return (getKth(nums1, 0, n - 1, nums2, 0, m - 1, left) + getKth(nums1, 0, n - 1, nums2, 0, m - 1, right)) * 0.5;  
    }
        private int getKth(int[] nums1, int start1, int end1, int[] nums2, int start2, int end2, int k) {
            int len1 = end1 - start1 + 1;
            int len2 = end2 - start2 + 1;
            //让 len1 的长度小于 len2，这样就能保证如果有数组空了，一定是 len1
            if (len1 > len2) return getKth(nums2, start2, end2, nums1, start1, end1, k);
            if (len1 == 0) return nums2[start2 + k - 1];
            if (k == 1) return Math.min(nums1[start1], nums2[start2]);
            int i = start1 + Math.min(len1, k / 2) - 1;
            int j = start2 + Math.min(len2, k / 2) - 1;
            if (nums1[i] > nums2[j]) {
                return getKth(nums1, start1, end1, nums2, j + 1, end2, k - (j - start2 + 1));
            }
            else {
                return getKth(nums1, i + 1, end1, nums2, start2, end2, k - (i - start1 + 1));
            }
        }
}
```
**时间复杂度：** $$O(log(m+n)$$

## 总结

自己还是太naive了
