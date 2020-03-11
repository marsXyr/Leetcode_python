# Leetcode 面试题 57-II 和为s的连续正数序列

***
### 题目描述

输入一个正整数 `target` ，输出所有和为 `target` 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。


**示例1：**

	输入：target = 9
	输出：[[2,3,4],[4,5]]
	
	
**示例2：**

	输入：target = 15
	输出：[[1,2,3,4,5],[4,5,6],[7,8]]


**说明：**

* `1 <= target <= 10^5`


**考点**

数学

### 代码
执行用时: **44ms**, 内存消耗: **13.7MB**

```
class Solution:
    def findContinuousSequence(self, target: int) -> List[List[int]]:
        n, res, ans = 2, 1, []
        while n ** 2 < 2 * target:
            if (target - res) % n == 0:
                ans.append([num for num in range((target - res) // n, (target - res) // n + n)])
            res += n
            n += 1
        return ans[::-1]
```



