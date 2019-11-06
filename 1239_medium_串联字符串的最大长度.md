# Leetcode 1239 串联字符串的最大长度
***
### 题目描述

给定一个字符串数组 `arr`，字符串 `s` 是将 `arr` 某一子序列字符串连接所得的字符串，如果 `s` 中的每一个字符都只出现过一次，那么它就是一个可行解。

请返回所有可行解 `s` 中最长长度。

**示例1:**

	输入：arr = ["un","iq","ue"]
	输出：4
	解释：所有可能的串联组合是 "","un","iq","ue","uniq" 和 "ique"，最大长度为 4。

**示例2：**

	输入：arr = ["cha","r","act","ers"]
	输出：6
	解释：可能的解答有 "chaers" 和 "acters"。
	
**示例3:**
	
	输入：arr = ["abcdefghijklmnopqrstuvwxyz"]
	输出：26

**提示：**

* `1 <= arr.length <= 16`
* `1 <= arr[i].length <= 26`
* `arr[i]` 中只含有小写英文字母

### 考点

位运算、回溯算法


### 思路
先把字符串数组 `arr` 中含有相同字符的字符串去掉。然后递归操作: `idx` 表示当前字符串数组位置，`maxStr` 表示当前最长字符串

* 如果 `idx >= len(new_arr)` ，说明已经遍历结束，返回当前最长字符串的最大值
* 如果 `not (set(maxStr) & set(new_arr[idx]))` ，说明当前遍历的字符串跟最长字符串没有重复字母，此时分两种情况，一种是将最长字符串加上当前字符串，一种是不加（防止后续存在更长字符串与当前字符串有冲突).
* 如果 当前遍历的字符串跟最长字符串有重复字母，只能不加。


### 代码
执行用时: **132ms**, 内存消耗: **13.9MB**

```
class Solution:
    def maxLength(self, arr: List[str]) -> int:
        new_arr = []
        for s in arr:
            if len(s) == len(set(s)):
                new_arr.append(s)
        def dfs(idx, maxStr):
            if idx >= len(new_arr):
                return len(maxStr)
            else:
                if not (set(maxStr) & set(new_arr[idx])):
                    return max(dfs(idx+1, maxStr+new_arr[idx]), dfs(idx+1, maxStr))
                else:
                    return dfs(idx+1, maxStr)
        maxLen = dfs(0, '')
        return maxLen
```

### 代码2

```
class Solution:
    def maxLength(self, arr: List[str]) -> int:
        arr = list(filter(lambda x: len(x) == len(set([_ for _ in x])), arr))  # 过滤重复元素

        hmap = self.get_map(arr)
        hmap = self.get_map(sorted(hmap, key=lambda x: hmap[x], reverse=True))

        sorted_arr = list(hmap.keys())
        max_len = hmap[sorted_arr[0]] if len(sorted_arr) > 0 else 0
        
        for i in range(len(hmap)):
            s1 = set([_ for _ in sorted_arr[i]])
            for j in range(i+1, len(hmap)):
                s2 = set([_ for _ in sorted_arr[j]])
                if len(s1 & s2) <= 0:
                    s1 = s1 | s2
                    max_len = max(max_len, len(s1))

        return max_len

    def get_map(self, arr: List[str]):
        arr_lens, hmap = list(map(lambda x: len(x), arr)), {}
        for s, l in zip(arr, arr_lens):
            hmap[s] = l
        return hmap
```

