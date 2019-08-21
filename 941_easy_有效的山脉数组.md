# Leetcode 941 有效的山脉数组
***
### 题目描述

给定一个整数数组 `A`，如果它是有效的山脉数组就返回 `true`，否则返回 `false`。

让我们回顾一下，如果 A 满足下述条件，那么它是一个山脉数组：

* `A.length >= 3`
* 在 `0 < i < A.length - 1` 条件下，存在 `i` 使得：
	* `A[0] < A[1] < ... A[i-1] < A[i]`
	* `A[i] > A[i+1] > ... > A[B.length - 1]`


**示例1:**  

	输入：[2,1]
	输出：false
	
**示例2:**  

	输入：[3,5,5]
	输出：false

**示例3:**  

	输入：[0,3,2,1]
	输出：true

	
**提示：**

1. `0 <= A.length <= 10000`
2. `0 <= A[i] <= 10000`


### 考点

数组


### 代码
执行用时: **308ms**, 内存消耗: **15MB**

```
class Solution:
    def validMountainArray(self, A: List[int]) -> bool:
        if len(A) < 3:
            return False
        
        pre, peak = -1, -1
        flagA, flagD = 0, 0
        
        for i in range(1, len(A) - 1):
            if A[i-1] < A[i] < A[i+1]:
                flagA = 1
            elif A[i] > A[i-1] and A[i] > A[i+1]:
                peak = i
                flagA = 0
            elif A[i-1] > A[i] > A[i+1]:
                if flagA == 1:
                    return False
                flagD = 1
            else:
                return False
        return False if peak == -1 else True
```

### 代码2(思路2)

```
class Solution:
    def validMountainArray(self, A: List[int]) -> bool:
        l, r = 0, len(A)-1
        while l < r and A[l] < A[l+1]:
            l += 1
        while r > l and A[r] < A[r-1]:
            r -= 1
        return l == r and l != 0 and r != len(A)-1
```
