# Leetcode 面试题 56-II 数组中数字出现的次数 II
***
### 题目描述

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

**示例1：**    

	输入：nums = [3,4,3,3]
	输出：4
	
**示例2：**    

	输入：nums = [9,1,7,9,7,9,7]
	输出：1


	
**说明：**

* `1 <= nums.length <= 10000`
* `1 <= nums[i] < 2^31`


**考点**

位运算

### 代码1
执行用时: **36ms**, 内存消耗: **13.5MB**

```
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        from collections import Counter
        counts = Counter(nums)
        for num in set(nums):
            if counts[num] == 1:
                return num
```

### 代码2
```
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return (sum(set(nums)) * 3 - sum(nums)) // 2
```


### 代码3
```
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for i in range(32):
            cnt = 0  # 记录当前 bit 有多少个1
            bit = 1 << i  # 记录当前要操作的 bit
            for num in nums:
                if num & bit != 0:
                    cnt += 1
            if cnt % 3 != 0:
                # 不等于0说明唯一出现的数字在这个 bit 上是1
                res |= bit

        return res - 2 ** 32 if res > 2 ** 31 - 1 else res
```




