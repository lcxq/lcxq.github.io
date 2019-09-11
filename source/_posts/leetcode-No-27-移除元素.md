---
title: leetcode No.27 移除元素
top: false
cover: true
toc: true
mathjax: true
date: 2019-09-02 21:25:39
password:
summary:
tags:
 - leetcode
 - 算法
 - Java
categories: leetcode
---

# 移除元素

给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

**示例 1:**

```markdown
给定 nums = [3,2,2,3], val = 3,

函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。

你不需要考虑数组中超出新长度后面的元素。
```

**示例 2:**

```markdown
给定 nums = [0,1,2,2,3,0,4,2], val = 2,

函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

注意这五个元素可为任意顺序。

你不需要考虑数组中超出新长度后面的元素。
```

## 方法

也挺简单的题。我自己的思路如下，，设置两个指针a,b，a指针从头遍历，遇到需要删除的元素时，b指针从尾部搜索无需删除的元素复制到a。
遍历的过程中记录一下遇到过多少次待删元素，最后返回总长减去删除元素个数即可。

解释一下为什么要从尾部遍历b指针。例如示例二，如果从a指针当前位置向后遍历的话，那么index=4的3复制到index=2的2后，3仍然留在数组中，最后返回长度5则会返回两次3，而不会出现位于后方的元素4。

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int ptr = 0, i = nums.length - 1, length = 0;
        while (ptr < nums.length) {
            if (nums[ptr] == val) {
                length ++;
                // i = Math.max(i - 1, ptr + 1);
                for (; i > ptr; --i) {
                    if (nums[i] != val) {
                        nums[ptr] = nums[i--];
                        break;
                    }
                }
            }
            ptr ++;
        }
        return nums.length - length;
    }
}
```

ps：这种题如果解法时间复杂度不是O（n）的话就没什么意义了。
