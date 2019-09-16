# Leetcode 506 相对名次
***
### 题目描述

给出 **N** 名运动员的成绩，找出他们的相对名次并授予前三名对应的奖牌。前三名运动员将会被分别授予 “金牌”，“银牌” 和“ 铜牌”（"Gold Medal", "Silver Medal", "Bronze Medal"）。

(注：分数越高的选手，排名越靠前。)

**示例:**

	输入: [5, 4, 3, 2, 1]
	输出: ["Gold Medal", "Silver Medal", "Bronze Medal", "4", "5"]
	解释: 前三名运动员的成绩为前三高的，因此将会分别被授予 “金牌”，“银牌”和“铜牌” ("Gold Medal", "Silver Medal" and "Bronze Medal").
	余下的两名运动员，我们只需要通过他们的成绩计算将其相对名次即可。

**提示：**

1. N 是一个正整数并且不会超过 10000。
2. 所有运动员的成绩都不相同。

### 考点

数组


### 代码
执行用时: **100ms**, 内存消耗: **15.2MB**

```
class Solution:
    def findRelativeRanks(self, nums: List[int]) -> List[str]:
        nums_idxs = [[score, index] for index, score in enumerate(nums)]
        nums_idxs.sort(key=lambda x: x[0], reverse=True)
        res = ['' for _ in range(len(nums))]
        rank = ['Gold Medal', 'Silver Medal', 'Bronze Medal']
        for i in range(3, len(nums)):
            rank.append(str(i + 1))
        for i, x in enumerate(nums_idxs):
            res[x[1]] = rank[i]
        return res
```

