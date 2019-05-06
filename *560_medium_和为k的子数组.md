# Leetcode 560 和为k的子数组
***
### 题目描述
给定一个整数数组和一个整数 **k**，你需要找到该数组中和为 **k** 的连续的子数组的个数。


**示例：**   
	
	输入:nums = [1,1,1], k = 2
	输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
	
    	
**提示：**  

* 数组的长度为`[1, 20000]`。
* 数组中元素的范围是`[-1000, 1000]`，且整数 **k** 的范围是`[-1e7, 1e7]`。
	

### 考点

* 哈希表

### 思路    
参考别人的做法。  
通过`Prefix sum`来求解。假设我们令`P[i] = A[0] + A[1] + ... + A[i-1]`和`P[j] = A[0] + A[1] + ... + A[j-1]`，那么`P[j] - P[i] = A[i] + A[i+1] + ... + A[j-1]`。如果`P[j] - P[i] == S`的话，那么`[i, j]`就是我们需要的区间。所以我们对于每个`j`，我们只要计算有多少个`i`使得`P[j] - P[i] == S`，这样就可以得到以`P[j]`作为右区间并且和为`S`的区间数。对于`A`中的每个元素都做相同的处理，最后将结果累加。 在具体实现中，我们通过`hashtable`记录`P[j]`。初始化时需要注意当`P[j] == S, P[i] == 0`时，此时我们的`result = 1`，所以我们初始化`dict[0] = 1`


### 代码  
执行用时: **84ms**, 内存消耗: **15.4MB** 

```
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        hashtable = {0:1}
        count = 0
        add = 0
        for i in range(len(nums)):
            add += nums[i]
            count += hashtable.get(add - k, 0)
            hashtable[add] = hashtable.get(add, 0) + 1
        return count   
```









	
