# Leetcode 131 分割回文串
***
### 题目描述

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回 *s* 所有可能的分割方案。

**示例1:**

	输入: "aab"
	输出:
	[
      ["aa","b"],
      ["a","a","b"]
    ]


### 考点

递归/回溯


### 思路

#### 递归
eg:
	 
	aabb
	先考虑在第 1 个位置切割，a | abb
	这样我们只需要知道 abb 的所有结果，然后在所有结果的头部把 a 加入
	abb 的所有结果就是 [a b b] [a bb]
	每个结果头部加入 a，就是 [a a b b] [a a bb]
	
	aabb
	再考虑在第 2 个位置切割，aa | bb
	这样我们只需要知道 bb 的所有结果，然后在所有结果的头部把 aa 加入
	bb 的所有结果就是 [b b] [bb]
	每个结果头部加入 aa,就是 [aa b b] [aa bb]
	
	aabb
	再考虑在第 3 个位置切割，aab|b
	因为 aab 不是回文串，所有直接跳过
	
	aabb
	再考虑在第 4 个位置切割，aabb |
	因为 aabb 不是回文串，所有直接跳过
	
	最后所有的结果就是所有的加起来
	[a a b b] [a a bb] [aa b b] [aa bb]
	
#### 回溯
eg:

	aabb
	先考虑在第 1 个位置切割，a | abb
	把 a 加入到结果中 [a]
	
	然后考虑 abb
	先考虑在第 1 个位置切割，a | bb
	把 a  加入到结果中 [a a]
	
	然后考虑 bb
	先考虑在第 1 个位置切割，b | b
	把 b 加入到结果中 [a a b] 
	
	然后考虑 b
	先考虑在第 1 个位置切割，b | 
	把 b 加入到结果中 [a a b b] 
	
	然后考虑空串
	把结果加到最终结果中 [[a a b b]]
	
	回溯到上一层 
	考虑 bb
	考虑在第 2 个位置切割，bb |
	把 bb 加入到结果中 [a a bb] 
	
	然后考虑 空串
	把结果加到最终结果中 [[a a b b] [a a bb]]
	
	然后继续回溯



### 代码1(递归)
执行用时: **128ms**, 内存消耗: **14MB**

```
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        if len(s) == 0:
            return [[]]
        if len(s) == 1:
            return [[s]]
        res = []
        for i in range(1, len(s) + 1):
            left, right = s[:i], s[i:]
            if left == left[::-1]:
                right = self.partition(right)
                for j in range(len(right)):
                    res.append([left] + right[j])
        return res
```

### 代码2（回溯)

```
class Solution:
    def partition(self, s: str) -> List[List[str]]:
	def helper(s, tmp):
           if not s:
               res.append(tmp)
           for i in range(1, len(s) + 1):
               if s[:i] == s[:i][::-1]:
                   helper(s[i:], tmp + [s[:i]])
        helper(s, [])
        return res
```

