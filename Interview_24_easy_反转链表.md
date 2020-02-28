# Leetcode 面试题 24 反转链表
***
### 题目描述

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

**示例1：**    

	输入: 1->2->3->4->5->NULL
	输出: 5->4->3->2->1->NULL
	
**说明**

* `0 <= 节点个数 <= 5000`


**考点**

链表


### 代码（递归）
执行用时: **40ms**, 内存消耗: **18MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:                    
        if not head or not head.next: return head
        node = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return node
```

### 代码2（迭代）

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:                         
        pre, cur = None, head       
        while cur:
            temp = cur.next
            cur.next = pre
            pre = cur
            cur = temp        
        return pre
```








