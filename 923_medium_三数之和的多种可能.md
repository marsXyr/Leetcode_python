# Leetcode 923 三数之和的多种可能
***
### 题目描述

给定一个整数数组 `A`，以及一个整数 `target` 作为目标值，返回满足 `i < j < k` 且 `A[i] + A[j] + A[k] == target` 的元组 `i, j, k` 的数量。

由于结果会非常大，请返回 结果除以 `10^9 + 7` 的余数。


**示例1:**  

	输入：A = [1,1,2,2,3,3,4,4,5,5], target = 8
	输出：20
	解释：
	按值枚举（A[i]，A[j]，A[k]）：
	(1, 2, 5) 出现 8 次；
	(1, 3, 4) 出现 8 次；
	(2, 2, 4) 出现 2 次；
	(2, 3, 3) 出现 2 次。
	
**示例2:**  

	输入：A = [1,1,2,2,3,3,4,4,5,5], target = 8
	输出：20
	解释：
	按值枚举（A[i]，A[j]，A[k]）：
	(1, 2, 5) 出现 8 次；
	(1, 3, 4) 出现 8 次；
	(2, 2, 4) 出现 2 次；
	(2, 3, 3) 出现 2 次。
	
**提示：**  
 
1. `3 <= A.length <= 3000`
2. `0 <= A[i] <= 100`
3. `0 <= target <= 300`


### 考点

双指针

### 思路
这个问题不能想复杂 - - 因为 `0 <= A[i] <= 100` 而 `3 <= A.length <= 3000` ，肯定要处理重复元素。  
就用简单的排列组合求解吧。 对于 `a + b + c == target` 存在下面三种情况（组合问题，不考虑`a,b,c`顺序）：  

* `a == b == c`
* `a == b != c`
* `a < b < c`

因此我们首先用`dict`记录`A`中的元素以及元素的个数。然后通过`i`和`j`遍历`dict`。如果是第一种情况，我们对结果`res`累加 `dict[i] * (dict[i] - 1) * (dict[i] - 2)//6`；如果是第二种情况，就累加 `dict[i] * (dict[i] - 1)//2 * dict[k]`；如果是第三种情况，就累加`dict[i] * dict[j] * dict[k]`。


### 代码
执行用时: **100ms**, 内存消耗: **12.9MB**。

```
class Solution:
    def threeSumMulti(self, A: List[int], target: int) -> int:
        from collections import Counter
        res = 0
        counter = Counter(A)
        for i, c_i in counter.items():
            for j, c_j in counter.items():
                k = target - i - j
                if k not in counter:
                    continue
                c_k = counter[k]
                
                if i == j == k:
                    res += c_i * (c_i-1) * (c_i-2) // 6
                if i == j != k:
                    res += c_i * (c_i-1) * c_k // 2
                elif i < j and j < k:
                    res += c_i * c_j * c_k
        return res % (10**9+7)
```


