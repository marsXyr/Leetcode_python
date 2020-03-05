# Leetcode 面试题 45 把数组排成最小的数
***
### 题目描述

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

**示例1：**

	输入: [10,2]
	输出: "102"
	
**示例2：**

	输入: [3,30,34,5,9]
	输出: "3033459"


**说明：**

* `0 < nums.length <= 100`
* `输出结果可能非常大，所以你需要返回一个字符串而不是整数`
* `拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0`


**考点**

排序


### 代码
执行用时: **60ms**, 内存消耗: **13.3MB**

```
class Solution:
    def minNumber(self, nums: List[int]) -> str:
        nums = list(map(str, nums))
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] > nums[j] + nums[i]:
                    nums[i], nums[j] = nums[j], nums[i]
        return "".join(nums)
```

### 代码2

```
class cmpSmaller(str):
    def __lt__(self, y):
        return self + y < y + self  # 字符串拼接比较(两两比较)
    # 按由小到大来排列

class Solution:
    def minNumber(self, nums: List[int]) -> str:
        res=sorted(map(str, nums),key=cmpSmaller)
        return ''.join(res)
```







