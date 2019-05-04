# Leetcode 83 删除排序链表中的重复元素
***
### 题目描述
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

**示例1:**

	输入: 1->1->2
	输出: 1->2

**示例2:**

	输入: 1->1->2->3->3
	输出: 1->2->3

### 考点

* 链表操作


### 代码
执行用时: **64ms**, 内存消耗: **12.9MB**。


```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        p = head
        while p and p.next:
            if p.next.val != p.val:
                p = p.next
                continue
            else:
                p.next = p.next.next
                continue
        return head             
```
