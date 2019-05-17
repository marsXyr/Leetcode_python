# Leetcode 978 最长湍流子数组
***
### 题目描述
当 `A` 的子数组 `A[i], A[i+1], ..., A[j]` 满足下列条件时，我们称其为湍流子数组：

* 若 `i <= k < j`，当 `k` 为奇数时， `A[k] > A[k+1]`，且当 `k` 为偶数时，`A[k] < A[k+1]`；
* **或** 若 `i <= k < j`，当 `k` 为偶数时，`A[k] > A[k+1]` ，且当 `k` 为奇数时， `A[k] < A[k+1]`。

也就是说，如果比较符号在子数组中的每个相邻元素对之间翻转，则该子数组是湍流子数组。

返回 `A` 的最大湍流子数组的**长度**。


**示例1:**  

	输入：[9,4,2,10,7,8,8,1,9]
	输出：5
	解释：(A[1] > A[2] < A[3] > A[4] < A[5])
	
**示例2:**  

	输入：[4,8,12,16]
	输出：2

**示例3:**  

	输入：[100]
	输出：1

	
**提示:**  

1. `1 <= A.length <= 40000`
2. `0 <= A[i] <= 10^9`

### 考点

* 数组、动态规划


### 代码
执行用时: **200ms**, 内存消耗: **18.3MB**。

```
class Solution:
    def maxTurbulenceSize(self, A: List[int]) -> int:
        lA = len(A)
        if lA <= 2:
            if lA == 2 and A[0] != A[1]:
                return 2
            else:
                return 1
        if len(set(A)) == 1:
            return 1
        sym = [0] * (lA - 1)
        for i in range(1, lA):
            if A[i] - A[i-1] > 0:
                sym[i-1] = 1
            elif A[i] - A[i-1] == 0:
                sym[i-1] = 0
            else:
                sym[i-1] = -1
        maxL, cur = 1, 1
        for i in range(1, lA-1):
            if sym[i] == sym[i-1] or sym[i] == 0:
                maxL = max(maxL, cur)
                if sym[i] == 0:
                    cur = 0
                else:
                    cur = 1            
            else:
                cur += 1
        return max(maxL, cur) + 1
```

### 代码(执行用时：148ms)
```
class Solution:
    def maxTurbulenceSize(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        count,maximum,L=0,0,len(A)
        if L<=2 :
            return L
        last=A[0]-A[1]
        for i in range(1,L-1) :
            count+=1
            now=A[i]-A[i+1]
            if last*now>=0:
                if maximum<count :
                    maximum=count
                count=0
            last=now
        for i in range(0,L-1):
            if A[i]!=A[i+1] :
                return max(maximum,count+1)+1
        return 1
```

