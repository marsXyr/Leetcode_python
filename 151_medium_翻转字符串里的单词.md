# Leetcode 151 翻转字符串里的单词
***
### 题目描述
给定一个字符串，逐个翻转字符串中的每个单词。

**示例1:**

	输入: "the sky is blue"
	输出: "blue is sky the"
 

**示例2:**

	输入: "  hello world!  "
	输出: "world! hello"
	解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。

**示例3:**

	输入: "a good   example"
	输出: "example good a"
	解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
    	
**说明：**  

* 无空格字符构成一个单词。
* 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
* 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
	

### 考点

* 字符串


### 代码  
执行用时: **52ms**, 内存消耗: **13.3MB** 

```
class Solution:
    def reverseWords(self, s: str) -> str:
        return " ".join([t for t in s.strip().split()][::-1])
```






	
