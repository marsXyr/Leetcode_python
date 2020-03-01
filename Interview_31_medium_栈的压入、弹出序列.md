# Leetcode 面试题 31 栈的压入、弹出序列
***
### 题目描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。


**示例1：**    

	输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
	输出：true
	解释：我们可以按以下顺序执行：
	push(1), push(2), push(3), push(4), pop() -> 4,
	push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1


**示例2：**

	输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
	输出：false
	解释：1 不能在 2 之前弹出。

**说明：**

* `0 <= pushed.length == popped.length <= 1000`
* `0 <= pushed[i], popped[i] < 1000`
* `pushed 是 popped 的排列。`


**考点**

栈


### 代码
执行用时: **64ms**, 内存消耗: **13.6MB**

```
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        stack = []
        while pushed:
            stack.append(pushed.pop(0))
            while stack and stack[-1] == popped[0]:
                stack.pop()
                popped.pop(0)
        return True if not stack else False
```








