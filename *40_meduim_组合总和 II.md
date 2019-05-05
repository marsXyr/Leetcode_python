# Leetcode 40 组合总和 II
***
### 题目描述
给定一个数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用一次。

**说明：**  

* 所有数字（包括目标数）都是正整数。
* 解集不能包含重复的组合。

**示例1:**

	输入: candidates = [10,1,2,7,6,1,5], target = 8,
	所求解集为:
	[
  		[1, 7],
  		[1, 2, 5],
  		[2, 6],
  		[1, 1, 6]
	]

**示例2:**

	输入: candidates = [2,5,2,1,2], target = 5,
	所求解集为:
	[
  		[1,2,2],
  		[5]
	]
	

### 考点

* 回溯法

### 思路   
先做一个剪枝操作，也就是只保留排序后的candidates中小于等于target的那部分。然后对这部分进行回溯操作(当target为0时，把part加入到res中需要先判断res中是否存在part，为方便判断，统一存储排序后的part)当前下标index < len(nums)且当前target大于等于nums[index]时，说明可以进行下一次回溯。


### 代码
执行用时: **144ms**, 内存消耗: **12.9MB**。


```
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates = sorted(candidates)
        res = [] 
        for i in range(len(candidates)):
            if candidates[i] > target:
                break
        l = i+1
        
        def dfs(nums, index, target, part):
            if target == 0:
                part = sorted(part)
                if part not in res: res.append(part)
                return
            if index == len(nums):
                return
            if index < len(nums) and target >= nums[index]:
                for i in range(index, len(nums)):
                    dfs(nums, i+1, target-nums[i], part+[nums[i]])
              
        dfs(candidates[:l], 0, target, [])
        return res  
```
