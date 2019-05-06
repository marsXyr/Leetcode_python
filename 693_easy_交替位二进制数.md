# Leetcode 693 交替位二进制数
***
### 题目描述
给定一个正整数，检查它是否为交替位二进制数：换句话说，就是它的二进制数相邻的两个位数永不相等。

**示例1:**   
	
	输入: 5
	输出: True
	解释:
	5的二进制数是: 101
	
**示例2:**   
	
	输入: 7
	输出: False
	解释:
	7的二进制数是: 111

**示例3:**   
	
	输入: 11
	输出: False
	解释:
	11的二进制数是: 1011
	
**示例4:**   
	
	输入: 10
	输出: True
	解释:
	10的二进制数是: 1010
	

### 考点

* 无


### 代码  
执行用时: **52ms**, 内存消耗: **13.2MB**

```
class Solution:
    def hasAlternatingBits(self, n: int) -> bool:
        bn = bin(n).replace('0b', '')
        for i in range(1, len(bn)):
            if bn[i] == bn[i-1]:
                return False
        return True              
```

### Smart Solution (36ms)
换一种写法

```
class Solution:
    def hasAlternatingBits(self, n: 'int') -> 'bool':
        a = bin(n)[2:]
        return not ('00' in a or '11' in a)
```







	
