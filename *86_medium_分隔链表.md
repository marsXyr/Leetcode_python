# Leetcode 86 分隔链表
***
### 题目描述

给定一个链表和一个特定值 x，对链表进行分隔，使得所有小于 x 的节点都在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

**示例：**

	输入: head = 1->4->3->2->5->2, x = 3
	输出: 1->2->2->4->3->5


### 考点

数组

### 思路
设置两个链表`minL`和`maxL`分别顺序存放小于`x`值和大于等于`x`值的节点。遍历链表得到`minL`和`maxL`后，再将两个新链表进行拼接即可。

### 代码
执行用时: **56ms**, 内存消耗: **12.9MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        if head == None:
            return head
        minL, maxL = ListNode(0), ListNode(0)
        p, q = minL, maxL
        while head:
            if head.val >= x:
                q.next = head
                q = q.next
            else:
                p.next = head
                p = p.next
            head = head.next
        p.next = maxL.next
        q.next = None
        return minL.next
```




