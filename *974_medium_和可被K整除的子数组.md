# Leetcode 974 和可被K整除的子数组
***
### 题目描述
给定一个整数数组 `A`，返回其中元素之和可被 `K` 整除的（连续、非空）子数组的数目。

**示例1：**

	输入：A = [4,5,0,-2,-3,1], K = 5
	输出：7
	解释：
	有 7 个子数组满足其元素之和可被 K = 5 整除：
	[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]

	
**提示：**

1. `1 <= A.length <= 30000`
2. `-10000 <= A[i] <= 10000`
3. `2 <= K <= 10000`

### 考点

哈希表，数学

### 思路
题目求连续子数组的和能被K整除，连续子数组的和就可以表示为前缀和的差，

比如 sum(A[i : j + 1]) = s[j + 1] - s[i]，

如果两个数的差能被K整除，就说明这两个数 mod K得到的结果相同，

只要找有多少对 mod k 相同的数就可以组合一下得到结果，

举例 对于A= [4,5,0,-2,-3,1] K = 5，

s = [0, 4, 9, 9, 7, 4, 5] ，

k = [2, 0, 1, 0, 4] 代表有s中有两个元素的余数都为0（即0和5），1个元素的余数为2（即7），四个元素的余数为4（即4994）

所以在保证余数相同的情况下，取出两个数都可以得到一组答案。对于这个例子答案就是 C22 + C12 + C42 = 1 + 0 + 6 = 7


### 代码
执行用时: **128ms**, 内存消耗: **15.7MB**

```
class Solution:
    def subarraysDivByK(self, A: List[int], K: int) -> int:
        
        s = [0 for i in range(len(A) + 1)]
        k = [0 for i in range(K)]
        
        for i in range(len(A)):
            s[i+1] = s[i] + A[i]
        
        for x in s:
            k[x % K] += 1
        
        return sum(x * (x - 1) // 2 for x in k)
```

### 代码2(哈希表，执行用时：144ms)

```
class Solution:
    def subarraysDivByK(self, nums: List[int], k: int) -> int:
        if len(nums)<1:
            return 0
        if k<0:
            k=-k
        pre_sum, res = 0, 0
        dic = {0:1}
        
        for val in nums:
            pre_sum = (pre_sum + val) % k
            if pre_sum in dic:
                res += dic[pre_sum]
            dic[pre_sum] = dic.get(pre_sum, 0) + 1
                
        return res 
```