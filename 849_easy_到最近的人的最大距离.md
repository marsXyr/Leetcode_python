# Leetcode 849 到最近的人的最大距离
***
### 题目描述
在一排座位（ `seats`）中，`1` 代表有人坐在座位上，`0` 代表座位上是空的。

至少有一个空座位，且至少有一人坐在座位上。

亚历克斯希望坐在一个能够使他与离他最近的人之间的距离达到最大化的座位上。

返回他到离他最近的人的最大距离。


**示例1:**  

	输入：[1,0,0,0,1,0,1]
	输出：2
	解释：
	如果亚历克斯坐在第二个空位（seats[2]）上，他到离他最近的人的距离为 2 。
	如果亚历克斯坐在其它任何一个空位上，他到离他最近的人的距离为 1 。
	因此，他到离他最近的人的最大距离是 2 。 
	
**示例2:**

	输入：[1,0,0,0]
	输出：3
	解释： 
	如果亚历克斯坐在最后一个座位上，他离最近的人有 3 个座位远。
	这是可能的最大距离，所以答案是 3 。

**提示：**

1. `1 <= seats.length <= 20000`
2. `seats` 中只含有 0 和 1，至少有一个 0，且至少有一个 1。


### 考点

数组


### 代码1
执行用时: **188ms**, 内存消耗: **14.3MB**

```
class Solution:
    def maxDistToClosest(self, seats: List[int]) -> int:
        maxzeros, curzeros = 0, 0      
        for i in range(len(seats)):
            if seats[i] == 0:
                curzeros += 1
            else:
                if curzeros > maxzeros:
                    maxzeros = curzeros
                curzeros = 0
        leftzeros = 0
        for i in range(len(seats)):
            if seats[i] == 0:
                leftzeros += 1
            else:
                break
        rightzeros = 0
        for i in range(len(seats)-1, -1, -1):
            if seats[i] == 0:
                rightzeros += 1
            else:
                break
        return max((maxzeros-1) // 2 + 1, leftzeros, rightzeros)
```

### 代码2(简洁)

```
class Solution:
    def maxDistToClosest(self, seats: List[int]) -> int:
        ones = [i for i, x in enumerate(seats) if x == 1]
        leftzeros = ones[0]
        rightzeros = len(seats) - 1 - ones[-1]
        midzeros = max([(ones[i] - ones[i-1]) // 2 for i in range(1, len(ones))] + [0])
        return max(leftzeros, midzeros, rightzeros)
```