# Leetcode 面试题 56-I 数组中数字出现的次数

***
### 题目描述

一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。


**示例1：**

	输入：nums = [4,1,4,6]
	输出：[1,6] 或 [6,1]
	
	
**示例2：**

	输入：nums = [1,2,10,4,1,4,3,3]
	输出：[2,10] 或 [10,2]


**说明：**

* `2 <= nums <= 10000`


**考点**

位运算

### 代码
执行用时: **68ms**, 内存消耗: **14.4MB**

```
class Solution:
    def singleNumbers(self, nums: List[int]) -> List[int]:
        xor, res = 0, [0, 0]
        for num in nums:
            xor ^= num
        low = -xor & xor
        for num in nums:
            res[not low & num] ^= num
        return res
```

### 代码2
```
class Solution:
    def singleNumbers(self, nums: List[int]) -> List[int]:
        res = set()
        for num in nums:
            if num in res: res.remove(num)
            else: res.add(num)
        return list(res)
```



