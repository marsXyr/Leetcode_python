# Leetcode 面试题 40 最小的k个数
***
### 题目描述

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

**示例1:**    

	 输入：arr = [3,2,1], k = 2
	 输出：[1,2] 或者 [2,1]
	
**示例2:**    

	 输入：arr = [0,1,2,1], k = 1
	 输出：[0]

	
**说明：**

* `0 <= k <= arr.length <= 1000`
* `0 <= arr[i] <= 1000`


### 考点

排序、堆

### 思路

1. 调用排序函数，时间复杂度为: O(nlogn).

2. 快排, 最差情况时间复杂度为: O(kn). 

3. 最小堆, 时间复杂度为: O(n) + O(klogn).   


### 代码
执行用时: **52ms**, 内存消耗: **14.3MB**

```
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        return sorted(arr)[:k]
        # return heapq.nsmallest(k, arr)
```

### 代码2(快排)
```
def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
      
        def partition(nums, low, high):
            pivot = nums[low]
            while low < high:
                while low < high and pivot <= nums[high]:
                    high -= 1
                nums[low] = nums[high]
                while low < high and pivot >= nums[low]:
                    low += 1
                nums[high] = nums[low]
            nums[low] = pivot
            return low
        
        if k > len(arr) or k <= 0: return []
        idx = partition(arr, 0, len(arr)-1)
        low, high = 0, len(arr)-1
        while idx != k-1:
            if idx < k-1:
                low = idx + 1
                idx = partition(arr, low, high)
            elif idx > k-1:
                high = idx - 1
                idx = partition(arr, low, high)
        return arr[:k]
```

### 代码3(最小堆)

```
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
     
        def heapAdjust(nums, k):
            n = len(nums)
            left = 2 * k + 1
            right = 2 * k + 2
            if left >= n: return
            minK = left
            if right < n and nums[left] > nums[right]:
                minK = right
            if nums[minK] < nums[k]:
                nums[minK], nums[k] = nums[k], nums[minK]
                heapAdjust(nums, minK)
        
        def heapSet(nums):
            n = len(nums)
            for i in range(n//2, -1, -1):
                heapAdjust(nums, i)
            return nums
        
        if k > len(arr) or k <= 0: return []
        minHeap = heapSet(arr)
        res = []
        for i in range(k):
            minHeap[0], minHeap[-1] = minHeap[-1], minHeap[0]
            res.append(minHeap.pop())
            heapAdjust(minHeap, 0)
        return res
```



