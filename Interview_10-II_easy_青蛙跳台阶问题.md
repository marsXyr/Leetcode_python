# Leetcode 面试题 10-II 青蛙跳台阶问题
***
### 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 `n` 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。


**示例1：**    

	输入：n = 2
	输出：2
	
**示例2：**

	输入：n = 7
	输出：21


	
**说明：**

* `0 <= n <= 100`


**考点**

递归


### 代码
执行用时: **48ms**, 内存消耗: **13.5MB**

```
from functools import lru_cache
class Solution:
    @lru_cache
    def numWays(self, n: int) -> int:
        if n == 0: return 1
        return n if n <= 2 else (self.numWays(n-1) + self.numWays(n-2)) % 1000000007   
```







