# Leetcode 275 H指数II
***
### 题目描述

给定一位研究者论文被引用次数的数组（被引用次数是非负整数），数组已经按照升序排列。编写一个方法，计算出研究者的 h 指数。

h 指数的定义: “h 代表“高引用次数”（high citations），一名科研人员的 h 指数是指他（她）的 （N 篇论文中）**至多**有 h 篇论文分别被引用了**至少** h 次。（其余的 N - h 篇论文每篇被引用次数**不多于** h 次。）"

**示例：**

	输入: citations = [0,1,3,5,6]
	输出: 3 
	解释: 给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 0, 1, 3, 5, 6 次。
		由于研究者有 3 篇论文每篇至少被引用了 3 次，其余两篇论文每篇被引用不多于 3 次，所以她的 h 指数是 3。

**说明：**      
如果 h 有多有种可能的值 ，h 指数是其中最大的那个。  


**进阶：**

* 这是 `H指数` 的延伸题目，本题中的 `citations` 数组是保证有序的。
* 你可以优化你的算法到对数时间复杂度吗？

### 考点

二叉搜索

### 思路 
时间复杂度为`O(n)`的算法很好实现，从后往前或从前往后遍历即可。  
但是如果要优化算法到时间复杂度`O(logn)`，则要考虑二分查找算法。  
注意在实现过程中，我们并不是找到一个满足条件:`citations[mid] >= l - mid`就立即返回了，而是要找到最大的`h`值，我们用`res`保存中间结果。


### 代码
执行用时: **48ms**, 内存消耗: **16.7MB**。

```
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        low, high, l = 0, len(citations) - 1, len(citations)
        res = 0
        while low <= high:
            mid = low + (high - low) // 2
            if citations[mid] >= l - mid:
                res = l - mid
                high = mid - 1
            elif citations[mid] < l - mid:
                low = mid + 1
        return res
```




