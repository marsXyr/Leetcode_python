# Leetcode 92 反转链表II
***
### 题目描述

反转从位置 *m* 到 *n* 的链表。请使用一趟扫描完成反转。


**示例1:**

    输入: 1->2->3->4->5->NULL, m = 2, n = 4
	输出: 1->4->3->2->5->NULL

	
**注意：**

1 ≤ m ≤ n ≤ 链表长度。

### 考点

链表

### 思路

* 先遍历到 m 位置，然后对 m 到 n 的每一个节点采用倒插法。


### 代码
执行用时: **32ms**, 内存消耗: **13.6MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
        count, p_pre, p = 1, ListNode(0), head
        p_pre.next = p
        while count < m:
            p_pre = p
            p = p.next
            count += 1
        while count < n:
            count += 1
            temp1 = p_pre.next
            temp2 = p.next
            q = p.next.next
            p_pre.next = temp2
            temp2.next = temp1
            p.next = q
        return p_pre.next if m < 2 else head
```

### 代码2(递归)

思路：用`left`和`right`分别表示`m`和`n`处所在节点，递归交换两个节点的数值。用递归方式处理`right`节点往前移动。

```
class Solution:
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """

        if not head:
            return None

        left, right = head, head
        stop = False
        def recurseAndReverse(right, m, n):
            nonlocal left, stop

            # base case. Don't proceed any further
            if n == 1:
                return

            # Keep moving the right pointer one step forward until (n == 1)
            right = right.next

            # Keep moving left pointer to the right until we reach the proper node
            # from where the reversal is to start.
            if m > 1:
                left = left.next

            # Recurse with m and n reduced.
            recurseAndReverse(right, m - 1, n - 1)

            # In case both the pointers cross each other or become equal, we
            # stop i.e. don't swap data any further. We are done reversing at this
            # point.
            if left == right or right.next == left:
                stop = True

            # Until the boolean stop is false, swap data between the two pointers     
            if not stop:
                left.val, right.val = right.val, left.val

                # Move left one step to the right.
                # The right pointer moves one step back via backtracking.
                left = left.next           

        recurseAndReverse(right, m, n)
        return head
```
