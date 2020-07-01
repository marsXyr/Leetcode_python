# Leetcode 969 煎饼排序
***
### 题目描述
给定数组 `A`, 我们可以对其进行 *煎饼翻转* : 我们选择一些正整数 `k <= A.length`, 然后反转 `A` 的 **前 k 个**元素的顺序。我们要执行零次或多次煎饼翻转（按顺序一次接一次地进行）以完成对数组 `A` 的排序。  

返回能使 `A` 排序的煎饼翻转操作所对应的 k 值序列。任何将数组排序且翻转次数在 `10 * A.length` 范围内的有效答案都将被判断为正确。

**示例1:**   
	
	输入：[3,2,4,1]
	输出：[4,2,4,3]
	解释：
	我们执行 4 次煎饼翻转，k 值分别为 4，2，4，和 3。
	初始状态 A = [3, 2, 4, 1]
	第一次翻转后 (k=4): A = [1, 4, 2, 3]
	第二次翻转后 (k=2): A = [4, 1, 2, 3]
	第三次翻转后 (k=4): A = [3, 2, 1, 4]
	第四次翻转后 (k=3): A = [1, 2, 3, 4]，此时已完成排序。

**示例2:**   
	
	输入：[1,2,3]
	输出：[]
	解释：
	输入已经排序，因此不需要翻转任何内容。
	请注意，其他可能的答案，如[3，3]，也将被接受。
	
	
**提示**

* `1 <= A.length <= 100`
* `A[i]` 是 `[1, 2, ..., A.length]` 的排列 

### 考点

* 数组操作


### 思路 
排序好的 `A` 是 `[1, 2, ..., A.length]`，因为煎饼排序只能翻转前`k`个，不影响后面的，那我们就依次从后往前排，比如现在待排 `i` ，那我们就找到数组`A`中 `i`的下标 `idx`，翻转下标 `0 到 idx` 的元素，这样就把 `i` 翻转到第一个位置, 然后我们再翻转下标`0 到 i-1`的元素，这样就把 `i` 元素翻转到了`i-1`位置。

### 代码  
执行用时 **60ms**, 内存消耗 **13.1MB**

```
class Solution:
    def pancakeSort(self, A: List[int]) -> List[int]:
        l = len(A)
        res = []
        while l:
            idx = A.index(l)
            if idx != l - 1:
                res.append(idx + 1)
                A[:idx+1] = A[idx::-1]
                res.append(l)
                A[:l] = A[l-1::-1]
                l -= 1
            else:
                l -= 1
        return res           
```

### Smart Solution

思路一样，就是写法不一样。

```
class Solution:
    def pancakeSort(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
            
        result = []
        for i in range(len(A), 0, -1):
            idx = A.index(i)
            result.extend([idx+1, i])
            A = A[idx:-1] + A[:idx]
        return result
``` 





	
