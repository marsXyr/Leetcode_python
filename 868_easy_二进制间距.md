# Leetcode 868 二进制间距
***
### 题目描述

给定一个正整数 `N`，找到并返回 `N` 的二进制表示中两个连续的 `1` 之间的最长距离。 

如果没有两个连续的 `1`，返回 `0` 。

**示例1：**

	输入：22
	输出：2
	解释：
	22 的二进制是 0b10110 。
	在 22 的二进制表示中，有三个 1，组成两对连续的 1 。
	第一对连续的 1 中，两个 1 之间的距离为 2 。
	第二对连续的 1 中，两个 1 之间的距离为 1 。
	答案取两个距离之中最大的，也就是 2 。

**示例2：**

	输入：5
	输出：2
	解释：
	5 的二进制是 0b101 。

**示例3：**

	输入：6
	输出：1
	解释：
	6 的二进制是 0b110 。

**示例4：**

	输入：8
	输出：0
	解释：
	8 的二进制是 0b1000 。
	在 8 的二进制表示中没有连续的 1，所以返回 0 。
	
**注意：**

* `1 <= N <= 10^9`

### 考点

数学

### 代码
执行用时: **40ms**, 内存消耗: **13MB**

```
class Solution:
    def binaryGap(self, N: int) -> int:
        bN = bin(N)
        maxGap, curGap = 0, 0
        idx = bN.find('1')
        if idx == -1:
            return 0
        for i in range(idx+1, len(bN)):
            if bN[i] == '0':
                curGap += 1
                continue
            else:
                curGap += 1
                if maxGap < curGap:
                    maxGap = curGap
                curGap = 0
        return maxGap
```

### 代码2(其他做法，执行用时：32ms)

```
class Solution:
    def binaryGap(self, N: int) -> int:
        A = [i for i in range(32) if (N >> i) & 1]
        if len(A) < 2: return 0
        return max(A[i+1] - A[i] for i in range(len(A) - 1))
```

