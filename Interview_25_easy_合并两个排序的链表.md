# Leetcode 面试题 25 合并两个排序的链表
***
### 题目描述

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

**示例1：**    

	输入：1->2->4, 1->3->4
	输出：1->1->2->3->4->4
	
**说明**

* `0 <= 链表长度 <= 1000`


**考点**

链表


### 代码（递归）
执行用时: **76ms**, 内存消耗: **15.6MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1: return l2
        if not l2: return l1
        if l1.val <= l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```

### 代码2（迭代）

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        new = ListNode(0)
        x = new
        while l1 and l2:
            if l1.val <= l2.val:
                x.next = l1
                l1 = l1.next
            else:
                x.next = l2
                l2 = l2.next
            x = x.next
        if l1: x.next = l1
        if l2: x.next = l2

        return new.next
```








