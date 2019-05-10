# Leetcode 698 划分为k个相等的子集
***
### 题目描述
给定一个整数数组 `nums` 和一个正整数 `k`，找出是否有可能把这个数组分成 `k` 个非空子集，其总和都相等。

**示例:**  

	输入： nums = [4, 3, 2, 3, 5, 2, 1], k = 4
	输出： True
	说明： 有可能将其分成 4 个子集（5），（1,4），（2,3），（2,3）等于总和。
	
**注意：**  

* `1 <= k <= len(nums) <= 16`
* `0 < nums[i] < 10000`
	

### 考点

* DFS

### 思路  
先判断一些基础的条件，比如：如果`k=1`那直接`return True`, 如果`sum(nums)%k`不等于`0`，那直接返回`False`，如果`len(nums)<k`,那么直接`return False`.  
然后进行DFS搜索，当本次搜索的`temp`等于`avg`时，说明划分了一个和为`avg`的子集，那么就进行下一次划分。注意`nums`数组是已排序的。用`visited`记录遍历过的数字，也就是每个子集中元素各不相同。


### 代码
执行用时: **40ms**, 内存消耗: **11.8MB**。


```
class Solution(object):
    def canPartitionKSubsets(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        if k == 1:
            return True
        total = sum(nums)
        if total % k != 0:
            return False
        avg = total // k
        nums.sort(reverse=True)
        n = len(nums)
        if n < k:
            return False
        visited = set()
        
        def dfs(k, temp, index):
            if temp == avg:
                return dfs(k-1, 0, 0)
            if k == 1:
                return True
            for i in range(index, n):
                if i not in visited and nums[i] + temp <= avg:
                    visited.add(i)
                    if dfs(k, temp+nums[i], i+1):
                        return True
                    visited.remove(i)
            return False
        return dfs(k, 0, 0)
```
