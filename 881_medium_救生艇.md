# Leetcode 881 救生艇
***
### 题目描述
第 `i` 个人的体重为 `people[i]`，每艘船可以承载的最大重量为 `limit`。

每艘船最多可同时载两人，但条件是这些人的重量之和最多为 `limit`。

返回载到每一个人所需的最小船数。(保证每个人都能被船载)。

**示例1：**

	输入：people = [1,2], limit = 3
	输出：1
	解释：1 艘船载 (1, 2)
	
**示例2：**

	输入：people = [3,2,2,1], limit = 3
	输出：3
	解释：3 艘船分别载 (1, 2), (2) 和 (3)

**示例3：**

	输入：people = [3,5,3,4], limit = 5
	输出：4
	解释：4 艘船分别载 (3), (3), (4), (5)
	
**提示：**

* `1 <= people.length <= 50000`
* `1 <= people[i] <= limit <= 30000`

### 考点

贪心算法+双指针

### 思路
对`people`按体重从大到小排序，设置双指针`left, right`，依次首尾相加，如果和小于等于`limit`，则可以乘船,`left+1, right+1`，否则就让体重大的乘船,`left+1`。

### 代码
执行用时: **192ms**, 内存消耗: **17.4MB**

```
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        people = sorted(people, reverse=True)
        left, right, res = 0, len(people) - 1, 0
        while left < right:
            if people[left] + people[right] <= limit:
                left, right = left + 1, right - 1
            else:
                left = left + 1
            res += 1
        return res + 1 if left == right else res
```

