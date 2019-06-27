# Leetcode 875 爱吃香蕉的珂珂
***
### 题目描述
珂珂喜欢吃香蕉。这里有 `N` 堆香蕉，第 `i` 堆中有 `piles[i]` 根香蕉。警卫已经离开了，将在 `H` 小时后回来。

珂珂可以决定她吃香蕉的速度 `K` （单位：根/小时）。每个小时，她将会选择一堆香蕉，从中吃掉 `K` 根。如果这堆香蕉少于 `K` 根，她将吃掉这堆的所有香蕉，然后这一小时内不会再吃更多的香蕉。  

珂珂喜欢慢慢吃，但仍然想在警卫回来前吃掉所有的香蕉。

返回她可以在 `H` 小时内吃掉所有香蕉的最小速度 `K`（`K` 为整数）。

**示例1：**

	输入: piles = [3,6,7,11], H = 8
	输出: 4

**示例2：**

	输入: piles = [30,11,23,4,20], H = 5
	输出: 30


**示例3：**

	输入: piles = [30,11,23,4,20], H = 6
	输出: 23

	
**提示：**

1. `1 <= piles.length <= 10^4`
2. `piles.length <= H <= 10^9`
3. `1 <= piles[i] <= 10^9`

### 考点

二分查找

### 思路
注意 二分查找 left 和 right 值的求解，线性方法比二分查找还快 - -

### 代码
执行用时: **428ms**, 内存消耗: **14.3MB**

```
class Solution:
    def minEatingSpeed(self, piles: List[int], H: int) -> int:
        left, right = sum(piles) // H, max(piles)
        while left < right:
            mid = (left + right) // 2
            if mid == 0:
                return 1
            count = sum((x-1) // mid + 1 for x in piles)
            if count <= H:
                right = mid
            else:
                left = mid + 1
        return left
```

### 代码2(优化后的，执行用时：60ms)

```
import math

class Solution:
    def minEatingSpeed(self, piles: List[int], H: int) -> int:
        left = math.ceil(sum(piles) / H)
        right = math.ceil(sum(piles) / (H - len(piles) + 1))
        while left < right:
            mid = left + (right - left) // 2
            if sum(map(lambda x : math.ceil(x / mid), piles)) <= H:
                right = mid
            else:
                left = mid + 1
        return left
```

### 代码3(线性求解，88ms)

```
class Solution:
    def minEatingSpeed(self, piles: List[int], H: int) -> int:
        for k in range(math.ceil(sum(piles) / H), max(piles) + 1):
            if sum((p - 1) // k + 1 for p in piles) <= H: return k
```
