# Leetcode 853 车队
***
### 题目描述
`N`  辆车沿着一条车道驶向位于 `target` 英里之外的共同目的地。

每辆车 `i` 以恒定的速度 `speed[i]` （英里/小时），从初始位置 `position[i]` （英里） 沿车道驶向目的地。

一辆车永远不会超过前面的另一辆车，但它可以追上去，并与前车以相同的速度紧接着行驶。

此时，我们会忽略这两辆车之间的距离，也就是说，它们被假定处于相同的位置。

*车队* 是一些由行驶在相同位置、具有相同速度的车组成的非空集合。注意，一辆车也可以是一个车队。

即便一辆车在目的地才赶上了一个车队，它们仍然会被视作是同一个车队。

 

会有多少车队到达目的地?


**示例:**

	输入：target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]
	输出：3
	解释：
	从 10 和 8 开始的车会组成一个车队，它们在 12 处相遇。
	从 0 处开始的车无法追上其它车，所以它自己就是一个车队。
	从 5 和 3 开始的车会组成一个车队，它们在 6 处相遇。
	请注意，在到达目的地之前没有其它车会遇到这些车队，所以答案是 3。
	
**提示：**  

1. `0 <= N <= 10 ^ 4`
2. `0 < target <= 10 ^ 6`
3. `0 < speed[i] <= 10 ^ 6`
4. `0 <= position[i] < target`
5. 所有车的初始位置各不相同。


### 考点

* 栈

### 思路   
题目说考点是栈，但是完全感觉用不到。先判断position长度如果小于等于1，直接返回。然后建一个数组ps，存储[剩余路程，所需时间]，然后按照剩余路程进行从小到大排序。然后遍历ps，比较剩余时间，如果剩余时间小于前一车队的剩余时间，则划分到前一车队，否则划分为一个新车队。


### 代码
执行用时: **108ms**, 内存消耗: **15.5MB**。


```
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        if len(position) <= 1:
            return len(position)
        ps = []
        for i in range(len(position)):
            dis = target - position[i]
            time = dis / speed[i]
            ps.append([dis, time])
        ps = sorted(ps, key=lambda x: x[0])
        count = 1
        t = ps[0][1]
        for i in range(1, len(ps)):
            if ps[i][1] <= t:
                continue
            else:
                count += 1
                t = ps[i][1]
        return count
```
