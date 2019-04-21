# Leetcode 477 汉明距离总和
***
### 题目描述
两个整数的`汉明距离`指的是这两个数字的二进制对应位不同的数量。  

计算一个数组中，任意两个数之间的汉明距离的综合。   

**示例1:**   
	
	输入: 4, 14, 2

	输出: 6

	解释: 在二进制表示中，4表示为0100，14表示为1110，2表示为0010。（这样表示是为了体现后四位之间关系）
	所以答案为：
	HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.

**提示**

* 数组中元素的范围为从`0`到`10^9`。
* 数组的长度不超过`10^4`。

### 考点

* 技巧/位操作

### 思路
统计二进制的0-31位，每位出现1的数字的数量，那么该位所有数字不同的数量就是该位出现1的数量乘以该位出现0的数量。

### 代码  
执行用时 **464ms**, 内存消耗 **14.3MB**

```
class Solution:
    def totalHammingDistance(self, nums: List[int]) -> int:
        total = 0
        for i in range(32):
            count1 = 0
            for num in nums:
                if num & (1 << i):
                    count1 += 1
            total += count1 * (len(nums) - count1)
        return total
              
```

### Smart Solution(192ms)
技巧型写法

```
class Solution:
    def totalHammingDistance(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ret = 0
        length = len(nums)
        num_strs = zip(*[bin(n)[2:].rjust(30, '0') for n in nums])
        
        for bit_group in num_strs:
            c1 = bit_group.count('0')
            ret += c1 * (length - c1)
        return ret
```





	