# Leetcode 面试题 51 数组中的逆序对
***
### 题目描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

**示例1：**

	输入: [7,5,6,4]
	输出: 5	
	

**说明：**

* `0 <= 数组长度 <= 50000`


**考点**

归并排序


### 代码
执行用时: **2268ms**, 内存消耗: **18MB**

```
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        self.counts = 0
        
        def merge(nums, start, mid, end, temp):
            i, j = start, mid+1
            while i <= mid and j <= end:
                if nums[i] <= nums[j]:
                    temp.append(nums[i])
                    i += 1
                else:
                    self.counts += mid - i + 1
                    temp.append(nums[j])
                    j += 1
            if i <= mid: temp += nums[i:mid+1]
            if j <= end: temp += nums[j:end+1]
            for i in range(len(temp)):
                nums[start+i] = temp[i]
            temp.clear()
        
        def mergesort(nums, start, end, temp):
            if start >= end: return
            mid = start + (end - start) // 2
            mergesort(nums, start, mid, temp)
            mergesort(nums, mid+1, end, temp)
            merge(nums, start, mid, end, temp)
        
        mergesort(nums, 0, len(nums)-1, [])
        return self.counts
```

### 代码2

```
class Solution:
    def reversePairs(self, nums: List[int]) -> int:
        L=[]
        ans=0
        for i in range(len(nums)):
            t=bisect.bisect_right(L,nums[i])
            ans+=i-t
            L[t:t]=[nums[i]]
        return ans
```


