# Leetcode 15 三数之和
***
### 题目描述
给定一个包含 *n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c* ，使得 *a + b + c = 0* ？找出所有满足条件且不重复的三元组。  

**注意：**答案中不可以包含重复的三元组。


**示例:**

	给定数组 nums = [-1, 0, 1, 2, -1, -4]，

	满足要求的三元组集合为：
	[
  	[-1, 0, 1],
  	[-1, -1, 2]
	]
	

### 考点

* 双指针


### 代码1(超时)
常人思路吧 - -


```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        if len(nums) < 3:
            return []
        nums = sorted(nums)
        lasti, lastj = nums[0] + 1, nums[1] + 1
        res = []
        for i in range(len(nums) - 2):
            if nums[i] >= 0:
                break
            if nums[i] == lasti:
                continue
            lasti = nums[i]
            lastj = nums[i+1]+1
            for j in range(i + 1, len(nums) - 1):
                if nums[i] + nums[j] >= 0:
                    break
                if nums[j] == lastj:
                    continue
                twoSum = nums[i] + nums[j]
                if -twoSum in nums[j + 1:]:
                    res.append([nums[i], nums[j], -twoSum])
                lastj = nums[j]
        if nums.count(0) >= 3:
            res.append([0,0,0])
        return res
            
```

### 代码2（执行用时: 1488ms, 内存消耗: 16.6MB）
双指针+优化

```
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        N = len(nums)
        nums.sort()
        res = []
        for t in range(N - 2):
            if t > 0 and nums[t] == nums[t - 1]:
                    continue
            i, j = t + 1, N - 1
            while i < j:
                _sum = nums[t] + nums[i] + nums[j]
                if _sum == 0:
                    res.append([nums[t], nums[i], nums[j]])
                    i += 1
                    j -= 1
                    while i < j and nums[i] == nums[i - 1]:
                        i += 1
                    while i < j and nums[j] == nums[j + 1]:
                        j -= 1
                elif _sum < 0:
                    i += 1
                else:
                    j -= 1
        return res
```

### 代码3（大佬做法, 执行用时: 396ms）

```
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        # 创建一个存储结果的列表
        res = []
        # 创建一个字典用于存储nums中的元素及其出现的次数
        d = dict()
        for i in nums:
            if i not in d:
                d[i] = 0
            d[i] += 1
        # 创建两个列表分别用于存储正数和负数
        posnum = [i for i in d if i > 0]
        negnum = [i for i in d if i < 0]
        # 如果nums中全为0，则返回0；
        if d.get(0, 0) > 2:
            res.append([0, 0, 0])
        if negnum == [] or posnum == []:
            return res
        # 分别对正数和负数两个列表中的值进行判断

        for i, x in enumerate(posnum):
            if d[x] >= 2 and -2 * x in d:
                res.append([x, x, -2 * x])
            for y in posnum[i + 1:]:
                if -(x + y) in d:
                    res.append([x, y, -x - y])
        for i, x in enumerate(negnum):
            if d[x] >= 2 and -2 * x in d:
                res.append([x, x, -2 * x])
            for y in negnum[i + 1:]:
                if -(x + y) in d:
                    res.append([x, y, -x - y])
        # 三个数之中有一个数为0 的情况
        if 0 in d:
            for x in posnum:
                if -x in d:
                    res.append([x, 0, -x])
        return res
```

### 代码4（大佬做法, 执行用时: 300ms）

```
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        #from collections import defaultdict
        from bisect import bisect_left, bisect_right
       
        target = 0
        
        result = []
        length = len(nums)
        
        if length < 3:
            return result
        
        count ={}
        # map the counts
        for n in nums:
            if n in count:
                count[n] += 1
            else:
                count[n] = 1
        keys = list(count.keys())
        keys.sort()
      
        t3 = target // 3
        if t3 in keys and count[t3] >= 3:
            result.append([t3, t3, t3])

        begin = bisect_left(keys, target - keys[-1] * 2)
        end = bisect_left(keys, target * 3)

        for i in range(begin, end):
            a = keys[i]
            if count[a] >= 2 and target - 2 * a in count:
                result.append([a, a, target - 2 * a])

            max_b = (target - a) // 2  # target-a is remaining
            min_b = target - a - keys[-1]  # target-a is remaining and c can max be keys[-1]
            b_begin = max(i + 1, bisect_left(keys, min_b))
            b_end = bisect_right(keys, max_b)

            for j in range(b_begin, b_end):
                b = keys[j]
                c = target - a - b
                if c in count and b <= c:
                    if b < c or count[b] >= 2:
                        result.append([a, b, c])
        return result
        
```




	