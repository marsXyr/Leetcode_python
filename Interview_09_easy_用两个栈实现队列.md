# Leetcode 面试题 09 用两个栈实现队列
***
### 题目描述

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

**示例1：**    

	输入：
	["CQueue","appendTail","deleteHead","deleteHead"]
	[[],[3],[],[]]
	输出：[null,null,3,-1]
	
**示例2：**

	输入：
	["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
	[[],[],[5],[2],[],[]]
	输出：[null,-1,null,null,5,2]


	
**说明：**

* `1 <= values <= 10000`
* `最多会对 appendTail、deleteHead 进行 10000 次调用`


**考点**

栈、队列


### 代码1
执行用时: **656ms**, 内存消耗: **16.9MB**

```
class CQueue:

    def __init__(self):
        self.stackIn = []
        self.stackOut = []

    def appendTail(self, value: int) -> None:
        self.stackIn.append(value)


    def deleteHead(self) -> int:
        if not self.stackOut:
            if not self.stackIn:
                return -1
            while self.stackIn:
                self.stackOut.append(self.stackIn.pop())
        return self.stackOut.pop()



# Your CQueue object will be instantiated and called as such:
# obj = CQueue()
# obj.appendTail(value)
# param_2 = obj.deleteHead()     
```







