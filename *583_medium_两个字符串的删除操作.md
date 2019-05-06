# Leetcode 583 两个字符串的删除操作
***
### 题目描述
给定两个单词 *word1* 和 *word2*，找到使得 *word1* 和 *word2* 相同所需的最小步数，每步可以删除任意一个字符串中的一个字符。


**示例:**   
	
	输入: "sea", "eat"
	输出: 2
	解释: 第一步将"sea"变为"ea"，第二步将"eat"变为"ea"
	
    	
**提示：**  

* 给定单词的长度不超过500。
* 给定单词中的字符只含有小写字母。
	

### 考点

* 动态规划

### 思路   
用动态规划求出两个字符串的最长公共子串（无需连续）。


### 代码  
执行用时: **380ms**, 内存消耗: **14.8MB** 

```
class Solution:
    def maxLongSubString(self, s1, l1, s2, l2):
        record = [[0 for _ in range(l2 + 1)] for _ in range(l1 + 1)]
        maxLen = 0
        for i in range (l1):
            for j in range(l2):
                if s1[i] == s2[j]:
                    record[i+1][j+1] = record[i][j] + 1
                else:
                    record[i+1][j+1] = max(record[i][j+1], record[i+1][j])
                    
        return record[l1][l2]
                        
    def minDistance(self, word1: str, word2: str) -> int:
        l1, l2 = len(word1), len(word2)
        sameLen = self.maxLongSubString(word1, l1, word2, l2)
        return (l1 + l2 - 2 * sameLen)               
```








	
