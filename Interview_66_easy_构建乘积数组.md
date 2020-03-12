# Leetcode 面试题 66 构建乘积数组

***
### 题目描述

给定一个数组 `A[0,1,…,n-1]`，请构建一个数组 `B[0,1,…,n-1]`，其中 `B` 中的元素 `B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]`。不能使用除法。


**示例1：**

	输入: [1,2,3,4,5]
	输出: [120,60,40,30,24]


**说明：**

* `所有元素乘积之和不会溢出 32 位整数`
* `a.length <= 100000`



**考点**

数组


### 代码
执行用时: **120ms**, 内存消耗: **23.1MB**

```
class Solution:
    def constructArr(self, a: List[int]) -> List[int]:
        L = len(a)
        left, right = [1] * L, [1] * L
        for i in range(1, L):
            left[i] = left[i-1] * a[i-1]
            right[L-i-1] = right[L-i] * a [L-i]
        return [left[i] * right[i] for i in range(L)]
```




