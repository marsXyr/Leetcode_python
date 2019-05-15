# Leetcode 457 环形数组循环
***
### 题目描述
给定一个含有正整数和负整数的环形数组 `nums`。 如果某个索引中的数 k 为正数，则向前移动 k 个索引。相反，如果是负数 (-k)，则向后移动 k 个索引。因为数组是环形的，所以可以假设最后一个元素的下一个元素是第一个元素，而第一个元素的前一个元素是最后一个元素。

确定 `nums` 中是否存在循环（或周期）。循环必须在相同的索引处开始和结束并且循环长度 > 1。此外，一个循环中的所有运动都必须沿着同一方向进行。换句话说，一个循环中不能同时包括向前的运动和向后的运动。


**示例1:**  

	输入：[2,-1,1,2,2]
	输出：true
	解释：存在循环，按索引 0 -> 2 -> 3 -> 0 。循环长度为 3 。

**示例2:**  

	输入：[-1,2]
	输出：false
	解释：按索引 1 -> 1 -> 1 ... 的运动无法构成循环，因为循环的长度为 1 。根据定义，循环的长度必须大于 1 。
	
**示例3:**  

	输入：[-2,1,-1,-2,-2]
	输出：false
	解释：按索引 1 -> 2 -> 1 -> ... 的运动无法构成循环，因为按索引 1 -> 2 的运动是向前的运动，
	而按索引 2 -> 1 的运动是向后的运动。一个循环中的所有运动都必须沿着同一方向进行。
	
**提示：**

1. -1000 ≤ nums[i] ≤ 1000
2. nums[i] ≠ 0
3. 1 ≤ nums.length ≤ 5000

### 考点

* 数组/双指针

### 思路  
暴力解法，分别写出当前值是正负的情况，用visited数组表示已经遍历过的位置。


### 代码
执行用时: **68ms**, 内存消耗: **12.9MB**。


```
class Solution:
    def circularArrayLoop(self, nums: List[int]) -> bool:
        visited = [0 for i in range(len(nums))]
        for i in range(len(nums)):
            if visited[i]:
                continue
            else:
                if nums[i] > 0:
                    cur = []
                    while i not in cur:
                        cur.append(i)
                        visited[i] = 1
                        if nums[i] < 0:
                            cur = []
                            break
                        i = (i + nums[i]) % len(nums)
                    if len(cur) > 1 and len(cur) - cur.index(i) > 1:
                        return True
                else:
                    cur = []
                    while i not in cur:
                        cur.append(i)
                        visited[i] = 1
                        if nums[i] > 0:
                            cur = []
                            break
                        i = (i + nums[i]) % len(nums)
                    if len(cur) > 1 and len(cur) - cur.index(i) > 1:
                        return True
        return False
```

### 代码2(双指针解法，执行用时：44ms)
```
class Solution:
    def circularArrayLoop(self, nums: 'List[int]') -> 'bool':
        n = len(nums)
        if n < 2:
            return False

        for i in range(n):

            cur = nums[i]

            if cur == 0:
                continue

            fast = (nums[i] + i) % n
            slow = i

            # 利用快慢指针判断是否有环
            # 原理：快慢指针，快指针走过的路，如果有环，慢指针肯定会走，则利用快指针控制循环
            # 如果两者相遇，判断是否会待在原地，如果不是，则存在
            while cur * nums[fast] > 0 and cur * nums[(nums[fast] + fast) % n] > 0:

                if fast == slow:
                    if slow == (nums[slow] + slow) % n:
                        break
                    return True

                fast = (nums[fast] + fast) % n
                fast = (nums[fast] + fast) % n
                slow = (nums[slow] + slow) % n
                

            nums[i] = 0
            next_index = (cur + i + n) % n
            if next_index == i:
                continue
            # 如果无环，则将能到达的位置标志为0，不再进入循环
            while cur * nums[next_index] > 0:
                cur = nums[next_index]
                nums[next_index] = 0
                next_index = (cur + next_index) % n            

        return False
```
