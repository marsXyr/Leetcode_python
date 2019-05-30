# Leetcode 88 合并两个有序数组
***
### 题目描述

给定两个有序整数数组 `nums1` 和 `nums2`，将 `nums2` 合并到 `nums1` 中，使得 `nums1` 成为一个有序数组。  

**说明：**   

* 初始化 `nums1` 和 `nums2` 的元素数量分别为 `m` 和 `n`。
* 你可以假设 `nums1` 有足够的空间（空间大小大于或等于 `m + n`）来保存 `nums2` 中的元素。

**示例:**  

	输入:
	nums1 = [1,2,3,0,0,0], m = 3
	nums2 = [2,5,6],       n = 3

	输出: [1,2,2,3,5,6]
	

### 考点

数组、双指针


### 代码1
执行用时: **1440ms**, 内存消耗: **13.2MB**。

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        i, j, index = m - 1, n - 1, m + n - 1
        while i >= 0 and j >= 0:
            if nums1[i] > nums2[j]:
                nums1[index] = nums1[i]
                i, index = i - 1, index - 1
            elif nums1[i] < nums2[j]:
                nums1[index] = nums2[j]
                j, index = j - 1, index - 1
            else:
                nums1[index], nums1[index-1] = nums1[i], nums1[i]
                i, j, index = i - 1, j - 1, index - 2
        if j >= 0:
            nums1[:j+1] = nums2[:j+1]
```

### 代码2(- -)

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums1[m:] = nums2
        nums1.sort()
```

