# Leetcode 面试题 10-I 斐波那契数列
***
### 题目描述

写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项。斐波那契数列的定义如下：

	F(0) = 0,   F(1) = 1
	F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。


**示例1：**    

	输入：n = 2
	输出：1
	
**示例2：**

	输入：n = 5
	输出：5


	
**说明：**

* `0 <= n <= 100`


**考点**

递归


### 代码（非递归）
执行用时: **24ms**, 内存消耗: **13.5MB**

```
class Solution:
    def fib(self, n: int) -> int:
        fbNums = [0, 1] + [0] * n
        for i in range(2, n+1):
            fbNums[i] = (fbNums[i-1] + fbNums[i-2]) % 1000000007
        return fbNums[n] 
```

### 代码2（递归）

```
from functools import lru_cache
class Solution:
    @lru_cache(None)
    def fib(self, n: int) -> int:
        return n if n < 2 else (self.fib(n-1) + self.fib(n-2)) % 1000000007
```







