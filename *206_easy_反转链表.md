# Leetcode 206 反转链表
***
### 题目描述

反转一个单链表。

**示例:**

	输入: 1->2->3->4->5->NULL
	输出: 5->4->3->2->1->NULL

**进阶：**

你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

### 考点

链表


### 代码1(迭代)
执行用时: **48ms**, 内存消耗: **14.7MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        p, q = head, None
        while p:
            temp = p.next
            p.next = q
            q = p
            p = temp
        return q
```

### 代码2(递归)

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        def reverse(pre, cur):
            if not cur: return pre
            next = cur.next
            cur.next = pre
            return reverse(cur, next)
        return reverse(None, head)
```