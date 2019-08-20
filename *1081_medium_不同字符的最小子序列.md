# Leetcode 1081 不同字符的最小子序列
***
### 题目描述

返回字符串 `text` 中按字典序排列最小的子序列，该子序列包含 `text` 中所有不同字符一次。


**示例1:**  

	输入："cdadabcc"
	输出："adbc"
	
**示例2:**  

	输入："abcd"
	输出："abcd"

**示例3:**  

	输入："ecbacba"
	输出："eacb"

**示例4:**  

	输入："leetcode"
	输出："letcod"
	
**提示：**

1. `1 <= text.length <= 1000`
2. `text` 由小写英文字母组成

### 考点

字符串、栈


### 代码
执行用时: **80ms**, 内存消耗: **13.8MB**

```
class Solution:
    def smallestSubsequence(self, text: str) -> str:
        res = []
        for i, c in enumerate(text):
            if c in res:
                continue
            else:
                while res and ord(res[-1]) > ord(c) and text.find(res[-1], i) != -1:
                    res.pop()
                res.append(c)
                               
        return "".join(res)
```

