# Leetcode 1004 最大连续1的个数 III
***
### 题目描述
给定一个由若干个`0`和`1`组成的数组`A`, 我们最多可以将`K`个值从0变成1。  
返回仅包含1的最长(连续)子数组的长度。


**示例 1:**   
	
	输入: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
	输出: 6
	解释: [1,1,1,0,0,1,1,1,1,1,1]
	
	   	 
**示例 2:**   
	
	输入: A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
	输出: 10
	解释: [0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
	
**提示:**   
	
	1. 1 <= A.length <= 20000
	2. 0 <= K <= A.length
	3. A[i] 为 0 或 1
	


### 考点

* 滑动窗口


### 代码  
执行用时 **276ms**, 内存消耗 **13.4MB**

```
class Solution:
    def longestOnes(self, A: List[int], K: int) -> int:
        left = 0  # 左窗口
        right = 0  # 右窗口
        count = K  
        res = 0  # 窗口大小
        while right < len(A):
            # 窗口大小最小为K, 先往右边将K个0变为1
            if(count > 0):
                if A[right] == 1:
                    right += 1
                else:
                    count -= 1
                    right += 1
            # 将窗口整体往右移
            else:
                if A[right] == 1:
                    right += 1
                else:
                    if A[left] == 1:
                        left += 1
                    else:
                        count += 1 
                        left += 1
            if right - left > res:
                res = right - left
        return res
```

### Smart Solution

```
class Solution:
    def longestOnes(self, A: List[int], K: int) -> int:
        l = 0
        for r, num in enumerate(A):
            K -= 1 - num
            if K < 0:
                K += 1 - A[l]
                l += 1
        return r - l + 1
```


	
