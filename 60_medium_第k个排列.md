# Leetcode 60 第k个排列
***
### 题目描述

给出集合 `[1,2,3,…,n]`，其所有元素共有 `n!` 种排列。

按大小顺序列出所有排列情况，并一一标记，当 `n = 3` 时, 所有排列如下：

1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`

给定 *n* 和 *k*，返回第 *k* 个排列。

**说明：**

* 给定 *n* 的范围是 [1, 9]。
* 给定 *k* 的范围是[1,  n!]。

**示例1:**  

	输入: n = 3, k = 3
	输出: "213"
	
**示例2:**  

	输入: n = 4, k = 9
	输出: "2314"


### 考点

数学、回溯


### 代码
执行用时: **52ms**, 内存消耗: **13.8MB**

```
class Solution:
    def getPermutation(self, n: int, k: int) -> str:
        # 每次只根据res值找出第一位应该排列的数字
        def helper(nums, res, ans):
            m = 1
            for i in range(len(nums)-1, 0, -1):
                m *= i
            c = (res - 1) // m
            ans += str(nums[c])
            res -= m * c      
            nums.pop(c)
            return nums, ans, res
        
        # 存放结果
        ans = ''
        # 每轮的"k"值
        res = k
        # 剩余待排元素
        nums = [i + 1 for i in range(n)]
        # 一共需要排列n个元素，所以进行n次
        for i in range(n, 0, -1):
            nums, ans, res = helper(nums, res, ans)
            
        return ans
```

