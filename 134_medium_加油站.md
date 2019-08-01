# Leetcode 134 加油站
***
### 题目描述
在一条环路上有 *N* 个加油站，其中第 *i* 个加油站有汽油 `gas[i]` 升。

你有一辆油箱容量无限的的汽车，从第 *i* 个加油站开往第 *i+1* 个加油站需要消耗汽油 `cost[i]` 升。你从其中的一个加油站出发，开始时油箱为空。

如果你可以绕环路行驶一周，则返回出发时加油站的编号，否则返回 -1。

**说明：**

* 如果题目有解，该答案即为唯一答案。
* 输入数组均为非空数组，且长度相同。
* 输入数组中的元素均为非负数。


**示例1:**

	输入: 
	gas  = [1,2,3,4,5]
	cost = [3,4,5,1,2]

	输出: 3

	解释:
	从 3 号加油站(索引为 3 处)出发，可获得 4 升汽油。此时油箱有 = 0 + 4 = 4 升汽油
	开往 4 号加油站，此时油箱有 4 - 1 + 5 = 8 升汽油
	开往 0 号加油站，此时油箱有 8 - 2 + 1 = 7 升汽油
	开往 1 号加油站，此时油箱有 7 - 3 + 2 = 6 升汽油
	开往 2 号加油站，此时油箱有 6 - 4 + 3 = 5 升汽油
	开往 3 号加油站，你需要消耗 5 升汽油，正好足够你返回到 3 号加油站。
	因此，3 可为起始索引。

**示例2:**  

	输入: 
	gas  = [2,3,4]
	cost = [3,4,3]

	输出: -1

	解释:
	你不能从 0 号或 1 号加油站出发，因为没有足够的汽油可以让你行驶到下一个加油站。
	我们从 2 号加油站出发，可以获得 4 升汽油。 此时油箱有 = 0 + 4 = 4 升汽油
	开往 0 号加油站，此时油箱有 4 - 3 + 2 = 3 升汽油
	开往 1 号加油站，此时油箱有 3 - 3 + 3 = 3 升汽油
	你无法返回 2 号加油站，因为返程需要消耗 4 升汽油，但是你的油箱只有 3 升汽油。
	因此，无论怎样，你都不可能绕环路行驶一周。



### 考点

贪心算法


### 思路

代码1和2运行时间基本一样 - -， 代码1的时间复杂度是O(n).

`res`数组保存`gas`与`cost`的差值。`i`从0开始遍历，如果`res[i]<0`, 那么跳过。否则, `j`从`i`开始遍历，如果`total`小于0，则break，`i`从`j`处继续遍历(类似于剪枝操作)。如果`j`能遍历到`L-1`，则说明`i`就是要找的位置。


### 代码1
执行用时: **80ms**, 内存消耗: **15.1MB**

```
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:     
        L = len(gas)
        res = [gas[i] - cost[i] for i in range(L)]
        if sum(res) < 0:
            return -1
        i = 0
        while i < L:
            if res[i] < 0:
                i += 1
                continue
            j, total, flag = i, 0, 0
            while j < L:
                total += res[j]
                if total < 0:
                    i = j
                    flag = 1
                    break
                j += 1
            if flag == 1:
                continue
            return i
        return -1
```

### 代码2(执行用时：28ms)

```
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        total, cur, start = 0, 0, 0
        for i in range(len(gas)):
            total += gas[i]-cost[i]
            cur += gas[i]-cost[i]
            if cur < 0:
                cur = 0
                start =i+1
        if cur >= 0 and total >= 0:
            return start
        return -1
```