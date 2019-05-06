# Leetcode 416 分割等和子集
***
### 题目描述
给定一个**只包含正整数**的**非空**数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**注意：**  

1. 每个数组中的元素不会超过 100
2. 数组的大小不会超过 200

**示例1:**

	输入: [1, 5, 11, 5]

	输出: true

	解释: 数组可以分割成 [1, 5, 5] 和 [11].
 

**示例2:**

	输入: [1, 2, 3, 5]

	输出: false

	解释: 数组不能分割成两个元素和相等的子集.
	

### 考点

* 深度优先搜索+剪枝 / 动态规划


### 代码(深度优先搜索+剪枝)  
执行用时: **56ms**, 内存消耗: **13.1MB** 

**思路：** 首先，我们要将`nums`中的元素加起来得到`sum(nums)`，然后进行取模运算，如果不能整除`2`的话，自然不可能满足条件。如果能整除，  
我们知道把`nums`划分为两个元素和相等的集合,`nums`中的元素要么属于一个集合，要么属于另一个集合。我们将两个集合中元素的和记为`cur1`, `cur2`。`index`表示目前元素的位置，那么`nums[index]`值要么加到`cur1`上，要么加到`cur2`上。我们只需要检查当`cur1`或者`cur2`等于`avg`时，就说明存在，返回`True`。当`cur1`或者`cur2`大于avg时，我们做剪枝处理，直接返回`False`。过程递归进行。

```
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sumNums = sum(nums)
        if sumNums % 2 != 0:
            return False
        avg = sumNums // 2
        
        def check(nums, cur1, cur2, index):
            if avg < cur1 or avg < cur2 or index == -1:
                return False
            if avg == cur1 or avg == cur2:
                return True
            return check(nums, cur1+nums[index], cur2, index-1) or check(nums, cur1, cur2+nums[index], index-1)
        
        return check(nums, 0, 0, len(nums)-1)
```

### 代码2（动态规划，比较耗时）

**思路：** 首先还是判断`nums`和是否能整除`2`。然后问题就转化为使用动态规划搜索容量为`sum(nums)/2`的背包是否能够装满

```
class Solution:
    def canPartition(self, nums: 'List[int]') -> 'bool':
    	sum_nums = sum(nums)

        if sum_nums % 2 != 0:
            return False
        avg = sum_nums // 2
        n = len(nums)
		
        dp = [[1] + [0] * avg for _ in range(n + 1)]
        for i in range(1, n + 1):
            for j in range(1, avg + 1):
                dp[i][j] = dp[i - 1][j]
                if j - nums[i - 1] >= 0:
                    if dp[i][j] == 0 and dp[i - 1][j - nums[i - 1]] == 1:
                        dp[i][j] = 1
        # print(dp)
        return True if dp[-1][-1] == 1 else False
```

### 代码3（大佬做法）

```
class Solution(object):

    def canPartition(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        sum_val = 0
        bits = 1
        for num in nums:
            sum_val += num
            bits |= bits << num

        return (not sum_val % 2 == 1) and (bits >> (sum_val // 2)) & 1 == 1
```






	
