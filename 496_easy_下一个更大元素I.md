# Leetcode 496 下一个更大元素 I
***
### 题目描述
给定两个**没有重复元素**的数组`nums1`和`nums2`, 其中`nums1`是`nums2`的子集。找到`nums1`中每个元素在`nums2`中的下一个比其大的值。  

`nums1`中数字 **x** 的下一个更大元素是指 **x** 在`nums2`中对应位置的右边的第一个比 **x** 大的元素。如果不存在，对应位置输出 -1。


**示例1:**   
	
	输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
	输出: [-1,3,-1]
	解释:
    	对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
    	对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
    	对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。
	
**示例2:**   
	
	输入: nums1 = [2,4], nums2 = [1,2,3,4].
	输出: [3,-1]
	解释:
    	对于num1中的数字2，第二个数组中的下一个较大数字是3。
    	对于num1中的数字4，第二个数组中没有下一个更大的数字，因此输出 -1。
    	
**注意：**  

* `nums1`和`nums2`中所有元素都是唯一的。
* `nums1`和`nums2`的数组大小都不超过1000。
	

### 考点

* 数组


### 代码  
执行用时: **104ms**, 内存消耗: **12.8MB**

```
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        res = []
        for x in nums1:
            idx = nums2.index(x)
            next_bigger = -1
            for i in range(idx+1, len(nums2)):
                if nums2[i] > x:
                    next_bigger = nums2[i]
                    break
            res.append(next_bigger)
        return res                    
```

### Smart Solution (44ms)
```
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        dmap = {}
        stack = []
        
        for n2 in nums2:
            while stack and stack[-1]<n2:
                dmap[stack.pop()] = n2
            stack.append(n2)
            
        return [dmap.get(n1,-1) for n1 in nums1]
```







	
