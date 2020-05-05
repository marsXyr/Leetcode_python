# Leetcode 4 寻找两个有序数组的中位数

***
### 题目描述

给定两个大小为 m 和 n 的有序数组 ``nums1`` 和 `` nums2``。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 ``O(log(m + n))``。

你可以假设 ``nums1`` 和 ``nums2`` 不会同时为空。



**示例1：**

	nums1 = [1, 3]
	nums2 = [2]
	
	则中位数是 2.0

**示例2：**

```
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```



**考点**

数组



**思路**

把本题转化为求解第k小的数，每次排除k/2个数，递归求解。

### 代码

执行用时: **68ms**, 内存消耗: **13.8MB**

```
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        
        def getKMin(nums1, start1, end1, nums2, start2, end2, k):
            l1, l2 = end1 - start1 + 1, end2 - start2 + 1
            if l1 == 0: return nums2[start2+k-1]
            if l2 == 0: return nums1[start1+k-1]
            if k == 1: return min(nums1[start1], nums2[start2])
            
            idx1 = start1 + min(l1, k//2) - 1
            idx2 = start2 + min(l2, k//2) - 1
            
            if nums1[idx1] < nums2[idx2]: 
                return getKMin(nums1, idx1+1, end1, nums2, start2, end2, k-(idx1-start1+1))
            else: 
                return getKMin(nums1, start1, end1, nums2, idx2+1, end2, k-(idx2-start2+1))   
        
        l1, l2 = len(nums1), len(nums2)
        left, right = (l1 + l2 + 1) // 2, (l1 + l2 + 2) // 2
        return (getKMin(nums1, 0, l1-1, nums2, 0, l2-1, left) + getKMin(nums1, 0, l1-1, nums2, 0, l2-1, right)) / 2.0
```



