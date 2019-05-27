# Leetcode 767 重构字符串
***
### 题目描述

给定一个字符串`S`，检查是否能重新排布其中的字母，使得两相邻的字符不同。

若可行，输出任意可行的结果。若不可行，返回空字符串。

**示例1:**  

	输入: S = "aab"
	输出: "aba"

**示例2:**  

	输入: S = "aaab"
	输出: ""
	
**示例3:**  

	输入: 10
	输出: false
	解释: 从右向左读, 为 01 。因此它不是一个回文数。
	
**注意：**  
 
* `S` 只包含小写字母并且长度在`[1, 500]`区间内。


### 考点

字符串、排序

### 思路

先统计每个字符的次数。然后判断出现最多次数的字符的数量与字符串S长度的关系，判断是否可以满足条件。  
然后分成下标为偶数位和奇数位，从偶数位0开始填入字符，然后再从奇数位开始填入剩余字符。

### 代码
执行用时: **52ms**, 内存消耗: **13MB**。

```
class Solution:
    def reorganizeString(self, S: str) -> str:
        from collections import Counter
        dic = Counter(S)
        if (dic.most_common(1)[0][1] >= (len(S) + 1) // 2 + 1):
            return ""
        dic = sorted(dic.items(), key=lambda x: x[1], reverse=True)
        new_S = ['a'] * len(S)
        index = 0
        for key, val in dic:
            while index < len(S) and val > 0:
                new_S[index] = key
                index += 2
                if index >= len(S):
                    index = 1
                val -= 1
        return ''.join(new_S)
```
