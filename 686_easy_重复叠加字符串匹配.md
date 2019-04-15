# Leetcode 686 重复叠加字符串匹配
***
### 题目描述
给定两个字符串 A 和 B，寻找重复叠加字符串 A 的最小次数，使得字符串 B 成为叠加后的字符串 A 的子串，如果不存在则返回 -1。  
举个例子，A = "abcd", B = "cdabcdab"。  
答案为3，因为 A 重复叠加三遍后为“abcdabcdabcd”，此时 B 是其子串；A 重复叠加两遍后为“abcdabcd”, B 并不是其子串。  


**注意:**   
	`A` 和 `B` 字符串的长度在1和10000区间范围内
	

### 考点

* 技巧


### 代码  
执行用时 **360ms**, 内存消耗 **13.2MB**

```
class Solution:
    def repeatedStringMatch(self, A: str, B: str) -> int:
        cnt = 1
        base = A
        while len(A) <= 10000:
            if B in A:
                return cnt
            A += base
            cnt += 1
        return -1
```

### Smart Solution

```
class Solution:
    def repeatedStringMatch(self, A, B):
        """
        :type A: str
        :type B: str
        :rtype: int
        """
        if len(set(A)) < len(set(B)):
            return -1
        q = (len(B) - 1) // len(A) + 1
        for i in range(2):
            if B in A * (q+i):
                return q+i
        return -1
```


	