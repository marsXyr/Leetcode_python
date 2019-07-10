# Leetcode 1109 航班预订统计
***
### 题目描述
这里有 `n` 个航班，它们分别从 `1` 到 `n` 进行编号。

我们这儿有一份航班预订表，表中第 `i` 条预订记录 `bookings[i] = [i, j, k]` 意味着我们在从 `i` 到 `j` 的每个航班上预订了 `k` 个座位。

请你返回一个长度为 `n` 的数组 `answer`，按航班编号顺序返回每个航班上预订的座位数。


**示例1:**

	输入：bookings = [[1,2,10],[2,3,20],[2,5,25]], n = 5
	输出：[10,55,45,25,25]
	

**说明：**

* `1 <= bookings.length <= 20000`
* `1 <= bookings[i][0] <= bookings[i][1] <= n <= 20000`
* `1 <= bookings[i][2] <= 10000`


### 考点

技巧(公交站点实时人数)


### 思路
暴力求解会超时。   
类似公交站点实时人数报数，`num`相当于公交车在每个站点实时人数，`begin`和`end`分别记录到第`i`站时上下车的人数。

### 代码
执行用时: **324ms**, 内存消耗: **22.8MB**

```
class Solution:
    def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
        
        begin = [0] * (n + 1)
        end = [0] * (n + 1)
        
        for i, j, k in bookings:
            begin[i] += k
            end[j] += k
        num = begin[1]
        res = [num]
        for i in range(2, n + 1):
            num += begin[i] - end[i-1]
            res.append(num)
        return res
```
