# Leetcode 491 递增子序列
***
### 题目描述

给定一个整型数组, 你的任务是找到所有该数组的递增子序列，递增子序列的长度至少是2。

**示例:**

	输入: [4, 6, 7, 7]
	输出: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]

**提示：**

1. 给定数组的长度不会超过15。
2. 数组中的整数范围是 [-100,100]。
3. 给定数组中可能包含重复数字，相等的数字应该被视为递增的一种情况.

### 考点

DFS


### 代码
执行用时: **332ms**, 内存消耗: **27.8MB**

```
class Solution:
    def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        self.res = set()
        L = len(nums)
        def dfs(idx, part):
            if len(part) >= 2 and part not in self.res:
                self.res.add(part)
            for i in range(idx+1, L):
                if part[-1] <= nums[i]:
                    dfs(i, part+(nums[i],))
        for i in range(L):
            dfs(i, (nums[i],))
        return [list(i) for i in self.res]
```

### 代码2

```
class Solution:
    def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        subs = {()}
        for num in nums:
            subs |= {sub + (num,)
                     for sub in subs
                     if not sub or sub[-1] <= num}
        return [sub for sub in subs if len(sub) >= 2]
```