# Leetcode 930 和相同的二元子数组
***
### 题目描述

在由若干 `0` 和 `1`  组成的数组 `A` 中，有多少个和为 `S` 的非空子数组。


**示例:**

	输入：A = [1,0,1,0,1], S = 2
	输出：4
	解释：
	如下面黑体所示，有 4 个满足题目要求的子数组：
	[1,0,1,0,1]
	[1,0,1,0,1]
	[1,0,1,0,1]
	[1,0,1,0,1]

**提示：**

1. `A.length <= 30000`
2. `0 <= S <= A.length`
3. `A[i]` 为 `0` 或 `1`

### 考点

哈希表、双指针

### 思路

[官方题解](https://leetcode-cn.com/problems/binary-subarrays-with-sum/solution/he-xiang-tong-de-er-yuan-zi-shu-zu-by-leetcode/)



### 代码1(前缀和)
执行用时: **376ms**, 内存消耗: **17.2MB**

```
class Solution:
    def numSubarraysWithSum(self, A: List[int], S: int) -> int:
        hashdic = {0: 1}
        sum_1, res = 0, 0
        for a in A:
            sum_1 += a
            if sum_1 - S in hashdic:
                res += hashdic[sum_1 - S]
            hashdic[sum_1] = hashdic.get(sum_1, 0) + 1
        return res
```

### 代码2(枚举子数组中1的位置)
```
class Solution:
    def numSubarraysWithSum(self, A: List[int], S: int) -> int:
        dt=[-1]
        for i in range(len(A)):
            if A[i]==1:
                dt.append(i)
        dt.append(len(A))  
        res=0
        if not S:
            for i in range(1,len(dt)-S):
                res+=(dt[i]-dt[i-1]-1)*((dt[i]-dt[i-1]))//2
        else:
            for i in range(1,len(dt)-S):
                res+=(dt[i]-dt[i-1])*(dt[i+S]-dt[i+S-1])
        return res
```

