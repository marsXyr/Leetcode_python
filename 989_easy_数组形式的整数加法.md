# Leetcode 989 数组形式的整数加法
***
### 题目描述
对于非负整数 `X` 而言， `X`的数组形式是每位数字按从左到右的顺序形成的数组。例如，如果 `X = 1231`, 那么其数组形式为 `[1,2,3,1]`。  

给定非负整数 `X` 的数组形式 `A`, 返回整数 `X+K` 的数组形式  

**示例1:**   
	
	输入: A = [1,2,0,0], K = 34
	输出: [1,2,3,4]
	解释: 1200 + 34 = 1234

**示例2:**   
	
	输入: A = [2,7,4], K = 181
	输出: [4,5,5]
	解释: 274 + 181 = 455
	
**示例3:**   
	
	输入: A = [2,1,5] K = 806
	输出: [1,0,2,1]
	解释: 215 + 806 = 1021
	
**示例4:**   
	
	输入: A = [9,9,9,9,9,9,9,9,9,9], K = 1
	输出: [1,0,0,0,0,0,0,0,0,0,0]
	解释: 9999999999 + 1 = 10000000000
	
**提示**

* `1 <= A.length <= 10000`
* `0 <= A[i] <= 9`
* `0 <= K <= 10000`
* 如果 `A.length > 1`, 那么 `A[0] != 0`

### 考点

* 无


### 思路 
先把数组A转换成数字，相加后，把结果再转换成数组

### 代码  
执行用时 **668ms**, 内存消耗 **13.3MB**

```
class Solution:
    def addToArrayForm(self, A: List[int], K: int) -> List[int]:
        m = len(A)
        a = 0
        for i in range(m):
            a = 10 * a + A[i]
        add = str(a + K)
        n = len(add)
        res = []
        for i in range(n):
            res.append(int(add[i]))
        return res            
```

### Smart Solution


```
class Solution:
    def addToArrayForm(self, A: 'List[int]', K: 'int') -> 'List[int]':
        for i in range(len(A))[::-1]:
            A[i], K = (A[i] + K) % 10, (A[i] + K) // 10
        if K:
            return [int(i) for i in str(K)] + A
        else:
            return A
``` 





	