# Leetcode 75 颜色分类
***
### 题目描述
给定一个包含红色、白色和蓝色，一共 *n* 个元素的数组，**原地**对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。


**说明：** 不能使用代码库中的排序函数来解决这道题。

**示例:**

	输入: [2,0,2,1,1,0]
	输出: [0,0,1,1,2,2]

**进阶：**

* 一个直观的解决方案是使用计数排序的两趟扫描算法。
首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
* 你能想出一个仅使用常数空间的一趟扫描算法吗？

	


### 考点

数组、双指针

### 思路

计数思路很直接也很简单，不再叙述。考虑一趟扫描算法。  
记`left`，`cur`，`right`，分别表示数组`0...left`已排序, 当前遍历位置，`right...len(nums)`已排序。  
遍历数组`nums`, 以1为分界线, 如果当前数字比1大，则将它跟数组末端元素互换`nums[cur], nums[right] = nums[right], nums[cur]`, 注意此时`right`要往前移一位；同理如果当前数字比1小，则将它跟数组起始端元素互换`nums[cur], nums[left] = nums[left], nums[cur]`, 注意此时`left`和`cur`都要往前移(因为互换后当前位置数字不会为2)；如果当前数字为1，则`cur += 1`



### 代码
执行用时: **44ms**, 内存消耗: **13.3MB**

```
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        left, cur, right = 0, 0, len(nums) - 1
        while cur <= right:
            if nums[cur] > 1:
                nums[cur], nums[right] = nums[right], nums[cur]
                right -= 1
            elif nums[cur] < 1:
                nums[cur], nums[left] = nums[left], nums[cur]
                left, cur = left + 1, cur + 1
            else:
                cur += 1
```

