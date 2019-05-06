# Leetcode 445 两数相加 II
***
### 题目描述
给定两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储单个数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

**进阶**:  
如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

**示例:**

	输入: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
	输出: 7 -> 8 -> 0 -> 7

### 考点

* 链表相加

### 思路  
把两个链表相加转化为两个字符串相加，相加结果再转化为链表形式。


### 代码
执行用时: **112ms**, 内存消耗: **13MB**。


```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        p, q = l1, l2
        ps, qs = "", ""
        
        while p:
            ps += str(p.val)
            p = p.next
        while q:
            qs += str(q.val)
            q = q.next
        rs = str(int(ps) + int(qs))
        head = ListNode(int(rs[0]))
        res = head
        for i in range(1, len(rs)):
            node = ListNode(str(rs[i]))
            head.next = node
            head = head.next
        return res            
```
