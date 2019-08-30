# Leetcode 826 安排工作以达到最大收益
***
### 题目描述

有一些工作：`difficulty[i]` 表示第`i`个工作的难度，`profit[i]`表示第`i`个工作的收益。

现在我们有一些工人。`worker[i]`是第`i`个工人的能力，即该工人只能完成难度小于等于`worker[i]`的工作。

每一个工人都最多只能安排一个工作，但是一个工作可以完成多次。

举个例子，如果3个工人都尝试完成一份报酬为1的同样工作，那么总收益为 3。如果一个工人不能完成任何工作，他的收益为 0 。

我们能得到的最大收益是多少？


**示例1:**

	输入: difficulty = [2,4,6,8,10], profit = [10,20,30,40,50], worker = [4,5,6,7]
	输出: 100 
	解释: 工人被分配的工作难度是 [4,4,6,6] ，分别获得 [20,20,30,30] 的收益。


**提示：**

* `1 <= difficulty.length = profit.length <= 10000`
* `1 <= worker.length <= 10000`
* `difficulty[i], profit[i], worker[i]`  的范围是 `[1, 10^5]`


### 考点

双指针

### 思路

排序`worker`和绑定`profit`和`difficulty`后排序`profit`，然后遍历`worker`,如果不大于`difficulty`，则此时的`profit`为最大。


### 代码
执行用时: **792ms**, 内存消耗: **16.1MB**

```
class Solution:
    def maxProfitAssignment(self, difficulty: List[int], profit: List[int], worker: List[int]) -> int:
        worker.sort(reverse=True)
        dp = sorted(zip(profit, difficulty))
        index, maxProfits = 0, 0
        for w in worker:
            while dp and dp[-1][1] > w:
                dp.pop()          
            if dp:
                maxProfits += dp[-1][0]
            else:
                break
        return maxProfits
```
