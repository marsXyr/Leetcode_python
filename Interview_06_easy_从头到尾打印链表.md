# Leetcode 面试题 06 从头到尾打印链表
***
### 题目描述

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例1：**    

	输入：head = [1,3,2]
	输出：[2,3,1]


	
**说明：**

* `0 <= 链表长度 <= 10000`


**考点**

链表


### 代码1
执行用时: **36ms**, 内存消耗: **13.4MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        if not head: return []
        res = []
        while head:
            res.append(head.val)
            head = head.next
        return res[::-1]      
```

### 代码2（递归）
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        if not head: return []
        return self.reversePrint(head.next) + [head.val]
```





