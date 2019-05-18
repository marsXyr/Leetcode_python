# Leetcode 551 学生出勤记录I
***
### 题目描述
给定一个字符串来代表一个学生的出勤记录，这个记录仅包含以下三个字符：

1. **'A'** : Absent，缺勤
2. **'L'** : Late，迟到
3. **'P'** : Present，到场
如果一个学生的出勤记录中**不超过一个'A'(缺勤)**并且**不超过两个连续的'L'(迟到)**,那么这个学生会被奖赏。

你需要根据这个学生的出勤记录判断他是否会被奖赏。


**示例1:**  

	输入: "PPALLP"
	输出: True
	
**示例2:**  

	输入: "PPALLL"
	输出: False

	
**提示:**  

1. `3 <= A.length <= 10000`
2. `1 <= A[i] <= 10^6`

### 考点

* 字符串


### 代码
执行用时: **36ms**, 内存消耗: **12.9MB**。

```
class Solution:
    def checkRecord(self, s: str) -> bool:
        return True if s.count('A') <= 1 and 'LLL' not in s else False            
```

