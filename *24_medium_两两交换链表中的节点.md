# Leetcode 24 两两交换链表中的节点
***
### 题目描述
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

**示例1:**

	给定 1->2->3->4, 你应该返回 2->1->4->3.


### 考点

递归、链表


### 代码
执行用时: **36ms**, 内存消耗: **13.7MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head
        nex = head.next
        head.next = self.swapPairs(nex.next)
        nex.next = head
        return nex
```