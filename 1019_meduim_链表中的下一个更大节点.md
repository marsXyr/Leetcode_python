# Leetcode 1019 链表中的下一个更大节点
***
### 题目描述
给出一个以头节点`head`作为第一个节点的链表。链表中的节点分别编号为`node_1, node_2, node_3, ...`。  

每个节点都可能有下一个更大值（*next larger*  **value**）：对于`node_i`，如果其`next_larger(node_i)`是`node_j.val`，那么就有`j > i`且`node_j.val > node_i.val`，而`j`是可能的选项中最小的那个。如果不存在这样的`j`，那么下一个更大值为`0`。  

返回整数答案数组`answer`，其中`answer[i] = next_larger(node_{i+1})`。  

**注意：**在下面的示例中，诸如`[2,1,5]`这样的**输入**（不是输出）是链表的序列化表示，其头节点的值为2，第二个节点的值为1，第三个节点的值为5。 

**示例1:**   
	
	输入：[2,1,5]
	输出：[5,5,0]

**示例2:**   
	
	输入：[2,7,4,3,5]
	输出：[7,0,5,5,0]
	
**示例3:**   
	
	输入：[1,7,5,1,9,2,5,1]
输出：[7,9,9,9,0,5,0,0]

**提示**

* 对于链表中的每个节点，`1 <= node.val <= 10^9`
* 给定列表的长度在`[0, 10000]`范围内

### 考点

* 链表操作

### 思路
定义一个栈stack，存储单调递减的序列，如果遇到下一个节点的值更大，则把栈中元素都pop出来，同时结果数组(res)中加入下一个节点的值或0（这里要定义一个largerval数组用来记录栈中出现的比下一个节点的值更大的值），遍历完后，再遍历res中出现0的值，因为每出现一个0就对应了largerval数组中的一个值val，然后找res中后续第一个大于val的值，然后改变res中原来的值(0)。最后检查栈中是否还有元素(因为最后可能是一个单调递减序列)，如果有的话就往res中加入0，最后再加入一个0（因为while head.next 步骤还剩最后一个元素没有遍历，这个时候只需要再往res中加入一个0就行）。

### 代码  
执行用时 **536ms**, 内存消耗 **17.6MB**

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def nextLargerNodes(self, head: ListNode) -> List[int]:
        if head == None or head.next == None:
            return [0]
        res = []
        stack = []
        largerval = []
        while head.next:
            stack.append(head.val)
            if head.val < head.next.val:
                cur = []
                curlarger = []
                while len(stack) > 0:                   
                    val = stack.pop()
                    if val < head.next.val:
                        cur.append(head.next.val)
                    else:
                        curlarger.append(val)
                        cur.append(0)
                res += cur[::-1]
                largerval += curlarger[::-1]
                
            head = head.next
        largerval = largerval[::-1]
        for i in range(len(res)):
            if res[i] == 0:
                val = largerval.pop()
                for j in range(i+1, len(res)):
                    if val < res[j]:
                        res[i] = res[j]
                        break
                      
        while len(stack) > 0:
            stack.pop()
            res.append(0)
        res.append(0)
        return res
              
```

### Smart Solution(416ms)

```
class Solution:
    def nextLargerNodes(self, head: ListNode) -> List[int]:
        pos = -1
        stack = []
        ans = []

        while head:
            pos += 1
            ans.append(0)
            while stack and stack[-1][1] < head.val:
                idx, _ = stack.pop()
                ans[idx] = head.val
            stack.append((pos, head.val))
            head = head.next
        return ans
```





	