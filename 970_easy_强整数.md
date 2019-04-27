# Leetcode 970 强整数
***
### 题目描述
给定两个正整数`x`和`y`，如果某一整数等于`x^i + y^j`，其中整数`i >= 0`且`j >= 0`，那么我们认为该整数是一个*强整数*。  

返回值小于等于`bound`的所有*强整数*组成的列表。  

你可以按任何顺序返回答案。在你的回答中，每个值最多出现一次。


**示例1:**   
	
	输入：x = 2, y = 3, bound = 10
	输出：[2,3,4,5,7,9,10]
	解释： 
	2 = 2^0 + 3^0
	3 = 2^1 + 3^0
	4 = 2^0 + 3^1
	5 = 2^1 + 3^1
	7 = 2^2 + 3^1
	9 = 2^3 + 3^0
	10 = 2^0 + 3^2
	

**示例2:**   
	
	输入：x = 3, y = 5, bound = 15
	输出：[2,4,6,8,10,14]
	
    	
**提示：**  

* `1 <= x <= 100`
* `1 <= y <= 100`
* `0 <= bound <= 10^6`
	

### 考点

* 穷举

### 思路    
暴力穷举，无奈代码基本一样，但别人用时40ms，而我用时68ms。- -


### 代码  
执行用时: **68ms**, 内存消耗: **13.2MB** 

```
class Solution:
    def powerfulIntegers(self, x: int, y: int, bound: int) -> List[int]:
        res = set()
        for i in range(101):
            if x ** i > bound:
                break
            for j in range(101):
                z = x ** i + y ** j
                if z <= bound:
                    res.add(z)
                else:
                    break
        return list(res)       
```









	