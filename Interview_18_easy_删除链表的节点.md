# Leetcode 面试题 18 删除链表的节点
***
### 题目描述

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

**示例1：**    

	 输入: head = [4,5,1,9], val = 5
	输出: [4,1,9]
	解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
	
**示例2：**

	输入: head = [4,5,1,9], val = 1
	输出: [4,5,9]
	解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.

	
**说明：**

* `题目保证链表中节点的值互不相同`
* `若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点`


### 考点

链表


### 代码（迭代）
执行用时: **52ms**, 内存消耗: **15MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if not head: return head
        if head.val == val: return head.next
        p, q = head, head.next
        while q and q.val != val:
            p = p.next
            q = q.next
        p.next = q.next
        return head
```

### 代码 (递归)
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, head: ListNode, val: int) -> ListNode:
        if not head: return head
        if head.val == val: return head.next
        head.next = self.deleteNode(head.next, val)
        return head
```


