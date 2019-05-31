# Leetcode 709 转换成小写字母
***
### 题目描述

实现函数 ToLowerCase()，该函数接收一个字符串参数 str，并将该字符串中的大写字母转换成小写字母，之后返回新的字符串。


**示例1:**  

	输入: "Hello"
	输出: "hello"
	
**示例2:**  

	输入: "here"
	输出: "here"
	
**示例3:**  

	输入: "LOVELY"
	输出: "lovely"


### 考点

字符串


### 代码
执行用时: **48ms**, 内存消耗: **12.9MB**。

```
class Solution:
    def toLowerCase(self, str: str) -> str:
        return str.lower()
```



