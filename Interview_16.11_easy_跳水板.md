# Leetcode 面试题 16.11 跳水板
***
### 题目描述

你正在使用一堆木板建造跳水板。有两种类型的木板，其中长度较短的木板长度为`shorter`，长度较长的木板长度为`longer`。你必须正好使用`k`块木板。编写一个方法，生成跳水板所有可能的长度。

返回的长度需要从小到大排列。

**示例:**

	输入：
	shorter = 1
	longer = 2
	k = 3
	输出： {3,4,5,6}

	
**说明：**

* `0 < shorter <= longer`
* `0 <= k <= 100000`


### 考点

递归、记忆化

### 思路

注意 `k == 0` 以及 `shorter == longer` 两种情况。

以及利用 **必须**使用 `k` 块木板的潜在含义.


### 代码
执行用时: **188ms**, 内存消耗: **19MB**

```
class Solution:
    def divingBoard(self, shorter: int, longer: int, k: int) -> List[int]:
        res = []
        if k < 1: return []
        if shorter == longer: return [k * shorter]
        for i in range(k + 1):         
            res.append(i * longer + (k - i) * shorter  )
        return res
```



