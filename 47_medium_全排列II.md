# Leetcode 47 全排列 II
***
### 题目描述
给定一个可包含重复数字的序列，返回所有不重复的全排列。

**示例1:**

	输入: [1,1,2]
	输出:
	[
      [1,1,2],
      [1,2,1],
      [2,1,1]
	]


### 考点

回溯


### 代码
执行用时: **128ms**, 内存消耗: **18MB**

```
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        from itertools import permutations
        
        return list(set(permutations(nums, len(nums))))
```

### 代码2(回溯法，执行用时：1540ms)

```
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        
        ans = []
        
        def back(res, k, part):
            if k == 0 and part not in ans:
                ans.append(part)
                return 
            elif k <= 0 or part in res:
                return 
            else:
                for i in range(k):
                    num = res[i]
                    back(res[:i] + res[i+1:], k - 1, part + [num])
            
        back(nums, len(nums), [])
        
        return ans
```

### 代码3(回溯法，执行用时：85ms)

```

class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res=[]
        def back(nums,t,res):
            if not nums:
                res.append(t)
            for i in range(len(nums)):
                if i>0 and nums[i-1]==nums[i]:
                    continue
                back(nums[:i]+nums[i+1:],t+[nums[i]],res)
        back(nums,[],res)
        return res
```