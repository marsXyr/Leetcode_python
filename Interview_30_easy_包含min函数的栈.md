# Leetcode 面试题 30 包含min函数的栈
***
### 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。
     
**示例：**    

	MinStack minStack = new MinStack();
	minStack.push(-2);
	minStack.push(0);
	minStack.push(-3);
	minStack.min();   --> 返回 -3.
	minStack.pop();
	minStack.top();      --> 返回 0.
	minStack.min();   --> 返回 -2.


**说明：**

* `各函数的调用总次数不超过 20000 次`


**考点**

栈


### 代码
执行用时: **96ms**, 内存消耗: **16.9MB**

```
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.min_stack = []


    def push(self, x: int) -> None:
        self.stack.append(x)   
        if not self.min_stack:
            self.min_stack.append(x)
        else:                       
            if x > self.min_stack[-1]:
                self.min_stack.append(self.min_stack[-1])
            else:
                self.min_stack.append(x)


    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()


    def top(self) -> int:
        return self.stack[-1]


    def min(self) -> int:
        return self.min_stack[-1]



# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.min()
```








