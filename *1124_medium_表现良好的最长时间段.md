# Leetcode 1124 表现良好的最长时间段
***
### 题目描述

给你一份工作时间表 `hours`，上面记录着某一位员工每天的工作小时数。

我们认为当员工一天中的工作小时数大于 `8` 小时的时候，那么这一天就是「**劳累的一天**」。

所谓「表现良好的时间段」，意味在这段时间内，「劳累的天数」是严格 **大于**「不劳累的天数」。

请你返回「表现良好时间段」的最大长度。


**示例1:**

	输入：hours = [9,9,6,0,6,6,9]
	输出：3
	解释：最长的表现良好时间段是 [9,9,6]。


**提示：**

* `1 <= hours.length <= 10000`
* `0 <= hours[i] <= 16`


### 考点

栈

### 思路

本题有多种方法，暴力的方法时间复杂度是 `O(N^2)`，用二分法可以将时间复杂度降为 `O(NlogN)` ，下面介绍用单调栈可以实现 `O(N)` 时间复杂度的方法。

以输入样例 `hours = [9,9,6,0,6,6,9]` 为例，我们将大于 `8` 小时的一天记为 `1` 分，小于等于 `8` 小时的一天记为 `−1` 分。那么我们转化为 `hours = [1, 1, -1, -1, -1, -1, 1]`，然后我们对得分数组计算前缀和 `PreSum = [0, 1, 2, 1, 0, -1, -2, -1]`。题目要求返回表现良好时间段的最大长度，即求最长的一段中，得分 `1` 的个数大于得分 `−1` 的个数，也就是求 `hours` 数组中最长的一段子数组，其和大于 `0`，那么也就是找出前缀和数组 `PreSum` 中两个索引 `i` 和 `j`，使 `j - i` 最大，且保证 `PreSum[j] - PreSum[i]` 大于 `0`。到此，我们就将这道题转化为，求 `PreSum` 数组中的一个最长的上坡，可以用单调栈实现。我们维护一个单调栈，其中存储 `PreSum` 中的元素索引，栈中索引指向的元素严格单调递减，由 `PreSum` 数组求得单调栈为 `stack = [0, 5, 6]`， 其表示元素为 `[0, -1, -2]`。然后我们从后往前遍历 `PreSum` 数组，与栈顶索引指向元素比较，如果相减结果大于 `0`，则一直出栈，直到不大于 `0` 为止，然后更新当前最大宽度。

### 代码
执行用时: **240ms**, 内存消耗: **13.6MB**

```
class Solution:
    def longestWPI(self, hours: List[int]) -> int:        
        PreSum = [0]
        curSum = 0       
        for i, x in enumerate(hours):
            curSum = curSum + 1 if x > 8 else curSum - 1
            PreSum.append(curSum)
        stack = []
        for i, x in enumerate(PreSum):
            if not stack or PreSum[stack[-1]] > x:
                stack.append(i)
        res, n = 0, len(hours)
        while n > res:
            while stack and PreSum[stack[-1]] < PreSum[n]:
                res = max(res, n - stack[-1])
                stack.pop()
            n -= 1
        return res
```



