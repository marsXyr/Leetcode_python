# Leetcode 11 盛最多水的容器

***
### 题目描述

给你 *n* 个非负整数 *a1，a2，…，an*，每个数代表坐标中的一个点 *(i, ai)* 。在坐标内画 *n* 条垂直线，垂直线 *i* 的两个端点分别为 *(i, ai)* 和 *(i, 0)*。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

<img src="images/7.png" width="300" height="120" >

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

**示例：**

	输入：[1,8,6,2,5,4,8,3,7]
	输出：49

**注意**

你不能倾斜容器，且 *n* 的值至少为 2。

**考点**

双指针

### 代码

执行用时: **44ms**, 内存消耗: **13.7MB**

```
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left, right = 0, len(height)-1
        res = 0
        while left < right:
            cur = (right - left) * min(height[left], height[right])
            res = max(res, cur)
            if height[left] < height[right]: left += 1
            else: right -= 1
        return res
```



