# Leetcode 55 跳跃游戏

***
### 题目描述

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

**示例1：**

	输入: [2,3,1,1,4]
	输出: true
	解释: 我们可以先跳 1 步，从位置 0 到达 位置 1, 然后再从位置 1 跳 3 步到达最后一个位置。

**示例2：**

```
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。
```



**考点**

贪心、数组

**思路**

从前往后遍历，判断当前最远可到达距离与index的关系：

1. 如果小于当前位置的index, 则无法到达最后
2. 如果大于最后位置的index, 则可以到达最后



### 代码

执行用时: **40ms**, 内存消耗: **13.8MB**

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        maxDis = 0
        for i, num in enumerate(nums):
            if maxDis < i: return False
            maxDis = max(maxDis, i+num)
            if maxDis >= len(nums)-1: return True
```



