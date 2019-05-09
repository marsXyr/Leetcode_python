# Leetcode 442 数组中重复的数据
***
### 题目描述
给定一个整数数组 a，其中1 ≤ a[i] ≤ n （n为数组长度）, 其中有些元素出现**两次**而其他元素出现**一次**。

找到所有出现**两次**的元素。

你可以不用到任何额外空间并在O(n)时间复杂度内解决这个问题吗？

**示例:**  

	输入:
	[4,3,2,7,8,2,3,1]

	输出:
	[2,3]
	

### 考点

* 数组


### 代码1
执行用时: **488ms**, 内存消耗: **18.9MB**。


```
class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = []
        nums = sorted(nums)
        for i in range(1, len(nums)):
            if nums[i] == nums[i-1]:
                res.append(nums[i])
        return res
```

### 代码2(技巧，执行用时: 480ms)
```
/*
 0 1 2 3 4 5 6 //数组序号
 7 7 4 2 4 1 1 //初始序列
            -1 //i=0, nums[abs(nums[0])-1] *= -1;
            +1 //i=1, nums[abs(nums[1])-1] *= -1;//7成对出现了。
      -2       //i=2, nums[abs(nums[2])-1] *= -1;
   -7          //i=3, nums[abs(nums[3])-1] *= -1;
      +2       //i=4, nums[abs(nums[4])-1] *= -1;//4成对出现了。
-7             //i=5, nums[abs(nums[5])-1] *= -1;
+7             //i=6, nums[abs(nums[6])-1] *= -1;//1成对出现了。
*/
class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        result = []
        for i in range(len(nums)):
            num = abs(nums[i])
            if nums[num-1] > 0:
                nums[num-1] *= -1
            else:
                result.append(num)
        return result
```

