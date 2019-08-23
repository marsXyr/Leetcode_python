# Leetcode 796 旋转字符串
***
### 题目描述

给定两个字符串, `A` 和 `B`。

`A` 的旋转操作就是将 `A` 最左边的字符移动到最右边。 例如, 若 `A = 'abcde'`，在移动一次之后结果就是`'bcdea'` 。如果在若干次旋转操作之后，`A` 能变成`B`，那么返回`True`。


**示例1:**

	输入: A = 'abcde', B = 'cdeab'
	输出: true

**示例2:**

	输入: A = 'abcde', B = 'abced'
	输出: false

**注意：**

* `A` 和 `B` 长度不超过 `100`。



### 考点

字符串


### 代码
执行用时: **40ms**, 内存消耗: **13.8MB**

```
class Solution:
    def rotateString(self, A: str, B: str) -> bool:
        
        i = 0
        tmp = A
        while i <= len(A):
            tmp = tmp[1:] + tmp[:1]
            if tmp == B:
                return True
            i += 1
        return False
```

### 代码2(简洁)

```
class Solution:
    def rotateString(self, A: str, B: str) -> bool:
        
        return len(A) == len(B) and B in A + A
```