# Leetcode 9 回文数
***
### 题目描述

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例1:**  

	输入: 121
	输出: true

**示例2:**  

	输入: -121
	输出: false
	解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
	
**示例3:**  

	输入: 10
	输出: false
	解释: 从右向左读, 为 01 。因此它不是一个回文数。
	
**进阶：**  
 
你能不将整数转为字符串来解决这个问题吗？


### 考点

数学


### 代码
执行用时: **100ms**, 内存消耗: **13.3MB**。

```
class Solution:
    def isPalindrome(self, x: int) -> bool:
        return str(x) == str(x)[::-1]
```

### 代码2(进阶)
思路：直观上来看待回文数的话，就感觉像是将数字进行对折后看能否一一对应。所以这个解法的操作就是 **取出后半段数字进行翻转**。这里需要注意的一个点就是由于回文数的位数可奇可偶，所以当它的长度是偶数时，它对折过来应该是相等的；当它的长度是奇数时，那么它对折过来后，有一个的长度需要去掉一位数（除以 10 并取整）。具体做法如下：      

* 每次进行取余操作 （ %10），取出最低的数字：`y = x % 10`
* 将最低的数字加到取出数的末尾：`revertNum = revertNum * 10 + y`
* 每取一个最低位数字，`x` 都要自除以 10
* 判断 `x` 是不是小于 `revertNum` ，当它小于的时候，说明数字已经对半或者过半了
* 最后，判断奇偶数情况：如果是偶数的话，`revertNum` 和 `x` 相等；如果是奇数的话，最中间的数字就在`revertNum` 的最低位上，将它除以 10 以后应该和 `x` 相等  

```
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if (x < 0) or (x % 10 == 0 and x != 0):
	    return False
	revertedNumber = 0
	while x > revertedNumber:
	    reveredNumber = revertedNumber * 10 + x % 10
	    x = x // 10
	return (x == revertedNumber) or (x == revertedNumber // 10)
```
