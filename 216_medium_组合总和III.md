# Leetcode 216 组合总和III
***
### 题目描述
找出所有相加之和为 **n** 的 **k** 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

**说明：**  

* 所有数字都是正整数。
* 解集不能包含重复的组合。


**示例1:**  

	输入: k = 3, n = 7
	输出: [[1,2,4]]
	
**示例2:**  

	输入: k = 3, n = 9
	输出: [[1,2,6], [1,3,5], [2,3,4]]


### 考点

* 回溯法


### 代码
执行用时: **48ms**, 内存消耗: **12.8MB**。

```
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
        if k > 9 or n > 45:
            return []
        res = []
        def backtrace(nums, index, cur, part):
            if cur == n and len(part) == k:
                res.append(part)
            if cur > n or len(part) > k:
                return
            for i in range(index, len(nums)):
                backtrace(nums, i+1, cur + nums[i], part + [nums[i]])
        backtrace(nums, 0, 0, [])
        
        return res          
```
