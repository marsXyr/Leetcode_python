# Leetcode 面试题 11 旋转数组的最小数字
***
### 题目描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  


**示例1：**    

	输入：[3,4,5,1,2]
	输出：1
	
**示例2：**

	输入：[2,2,2,0,1]
	输出：0

**考点**

二分查找


### 代码1（非二分查找）
执行用时: **52ms**, 内存消耗: **13.7MB**

```
class Solution:
    def minArray(self, numbers: List[int]) -> int:
        for i in range(1, len(numbers)):
            if numbers[i] < numbers[i-1]:
                return numbers[i]
        return numbers[0]  
```

### 代码2（二分查找）
```
class Solution:
    def minArray(self, numbers: List[int]) -> int:
        l, r = 0, len(numbers) - 1
        while l < r:
            mid = l + ((r - l) >> 1)
            # 右边大于中间，则右边一定是有序的
            if numbers[mid] < numbers[r]:
                r = mid
            elif numbers[mid] > numbers[r]:
                l = mid + 1
            else:
                r -= 1
        return numbers[l]
```






