# Leetcode 434 字符串中的单词数
***
### 题目描述
统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。  
请注意，你可以假定字符串里不包括任何不可打印的字符。 


**示例:**   
	
	输入: "Hello, my name is John"
	输出: 5
	

### 考点

* 字符串


### 代码  
执行用时 **48ms**, 内存消耗 **13.2MB**

```
class Solution:
    def countSegments(self, s: str) -> int:
        return len(s.split())               
```




	