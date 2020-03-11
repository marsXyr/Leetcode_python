# Leetcode 面试题 59-II 队列的最大值

***
### 题目描述

请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的**均摊**时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1


**示例1：**

	输入: 
	["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
	[[],[1],[2],[],[],[]]
	输出: [null,null,null,2,1,2]

**示例2：**

	输入: 
	["MaxQueue","pop_front","max_value"]
	[[],[],[]]
	输出: [null,-1,-1]


**说明：**

* `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
* `1 <= value <= 10^5`



**考点**

滑动窗口、队列

### 代码
执行用时: **272ms**, 内存消耗: **17MB**

```
class MaxQueue:

    def __init__(self):
        from collections import deque
        self.queue = deque()
        self.max_queue = deque()

    def max_value(self) -> int:
        return self.max_queue[0] if self.max_queue else -1

    def push_back(self, value: int) -> None:
        while self.max_queue and self.max_queue[-1] < value:
            self.max_queue.pop()
        self.max_queue.append(value)
        self.queue.append(value)

    def pop_front(self) -> int:
        if not self.queue: return -1
        if self.queue[0] == self.max_queue[0]:
            self.max_queue.popleft()
        return self.queue.popleft()
        

# Your MaxQueue object will be instantiated and called as such:
# obj = MaxQueue()
# param_1 = obj.max_value()
# obj.push_back(value)
# param_3 = obj.pop_front()
```



