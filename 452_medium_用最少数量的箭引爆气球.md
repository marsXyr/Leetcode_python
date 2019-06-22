# Leetcode 452 用最少数量的箭引爆气球
***
### 题目描述

在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以y坐标并不重要，因此只要知道开始和结束的x坐标就足够了。开始坐标总是小于结束坐标。平面内最多存在104个气球。

一支弓箭可以沿着x轴从不同点完全垂直地射出。在坐标x处射出一支箭，若有一个气球的直径的开始和结束坐标为 xstart，xend， 且满足  xstart ≤ x ≤ xend，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。



**示例1：**

	输入:
	[[10,16], [2,8], [1,6], [7,12]]

	输出:
	2

	解释:
	对于该样例，我们可以在x = 6（射爆[2,8],[1,6]两个气球）和 x = 11（射爆另外两个气球）。

### 考点

贪心算法

### 思路
对所有气球按end位置排序。遍历end，对于每一个end，箭数量加一，如果起始位置start小于等于end，则说明可以用一支箭引爆，删掉该气球的位置。

### 代码
执行用时: **176ms**, 内存消耗: **16.6MB**

```
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        points = sorted(points, key=lambda x: x[1])
        res = 0
        while len(points) > 0:
            end = points[0][1]
            res += 1
            while points and points[0][0] <= end:
                del (points[0])
        return res
```

### 代码2(执行用时：92ms)

```
class Solution:
    def findMinArrowShots(self, points: List[List[int]]) -> int:
        points.sort(key=lambda x: x[1])
        res, end = 0, float('-inf')
        for p in points:
            if p[0] > end:
                res += 1
                end = p[1]
        return res
```

