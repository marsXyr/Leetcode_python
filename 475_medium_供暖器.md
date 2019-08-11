# Leetcode 475 供暖器
***
### 题目描述

冬季已经来临。 你的任务是设计一个有固定加热半径的供暖器向所有房屋供暖。

现在，给出位于一条水平线上的房屋和供暖器的位置，找到可以覆盖所有房屋的最小加热半径。

所以，你的输入将会是房屋和供暖器的位置。你将输出供暖器的最小加热半径。

**说明：**

1. 给出的房屋和供暖器的数目是非负数且不会超过 25000。
2. 给出的房屋和供暖器的位置均是非负数且不会超过10^9。
3. 只要房屋位于供暖器的半径内(包括在边缘上)，它就可以得到供暖。
4. 所有供暖器都遵循你的半径标准，加热的半径也一样。


**示例1:**  

	输入: [1,2,3],[2]
	输出: 1
	解释: 仅在位置2上有一个供暖器。如果我们将加热半径设为1，那么所有房屋就都能得到供暖。

**示例2:**  

	输入: [1,2,3,4],[1,4]
	输出: 1
	解释: 在位置1, 4上有两个供暖器。我们需要将加热半径设为1，这样所有房屋就都能得到供暖。


### 考点

双指针

### 思路

计算所有房屋左右供暖器的最小值中的最大值

### 代码1
执行用时: **692ms**, 内存消耗: **17.2MB**

```
class Solution:
    def findRadius(self, houses: List[int], heaters: List[int]) -> int:
        houses.sort()
        heaters.sort()
        res = 0
        pre, Lh = 0, len(heaters)
        for x in houses:
            if x <= heaters[pre]:
                dis = heaters[pre] - x
            else:
                dis = abs(x - heaters[pre])
                if pre + 1 < Lh:
                    if heaters[pre+1] >= x:
                        dis = min(dis, heaters[pre+1] - x)
                    else:
                        while pre + 2 < Lh:
                            if heaters[pre+1] <= x:
                                pre += 1
                            else:
                                break
                        dis = min(dis, abs(heaters[pre] - x), abs(heaters[pre+1] - x))
            res = max(res, dis)
        return res
```

### 代码2(执行用时：100ms)

```
from typing import List


class Solution:
    def findRadius(self, houses: List[int], heaters: List[int]) -> int:
        if len(houses) == 0:
            return 0

        if len(heaters) == 0:
            raise Exception()

        houses.sort()

        # 供暖器加入两个极限值 +-inf
        inf = float("inf")
        heaters.append(inf)
        heaters.append(-inf)
        heaters.sort(reverse=True)

        last_heater = heaters.pop()
        next_heater = heaters.pop()

        max_radious = 0
        for house in houses:
            # 下一个供暖器要在房屋右边
            while next_heater < house:
                last_heater = next_heater
                next_heater = heaters.pop()

            last_distance = house - last_heater
            next_distance = next_heater - house

            radious = min(last_distance, next_distance)
            if radious > max_radious:
                max_radious = radious

        return max_radious
```