# Leetcode 29 两数相除
***
### 题目描述
给定两个整数，被除数 `dividend` 和除数 `divisor`。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 `dividend` 除以除数 `divisor` 得到的商。


**示例1:**  

	输入: dividend = 10, divisor = 3
	输出: 3
	
**示例2:**  

	输入: dividend = 7, divisor = -3
	输出: -2
	
**说明：**  

* 被除数和除数均为 32 位有符号整数。
* 除数不为 0。
* 假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。


### 考点

* 位运算

### 思路
题目中已经限制了不能用乘/除/取模运算，而如果用减法，那效率太低，会超时。所以我们只考虑效率高的位运算。  
我们可以把一个dividend（被除数）先除以2^n，n最初为31，不断减小n去试探,当某个n满足dividend/2^n>=divisor时，表示我们找到了一个足够大的数，这个数divisor是不大于dividend的，所以我们就可以减去2^n个divisor，以此类推
我们可以以100/3为例，2^n是1，2，4，8...2^31这种数，当n为31时，这个数特别大，100/2^n是一个很小的数，肯定是小于3的，所以循环下来，当n=5时，100/32=3, 刚好是大于等于3的，这时我们将100-32*3=4，也就是减去了32个3，接下来我们再处理4，同样手法可以再减去一个3，所以一共是减去了33个3，所以商就是33。最后我们需要处理一些越界情况。


### 代码
执行用时: **52ms**, 内存消耗: **13.1MB**。

```
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        flag = 1 if abs(dividend + divisor) != abs(dividend) + abs(divisor) else 0
        dividend, divisor, res = abs(dividend), abs(divisor), 0
        for i in range(31, -1, -1):
            if dividend >> i >= divisor:
                res += 1 << i
                dividend -= divisor << i
        if flag:
            return -2**31 if res >= 2**31 else -res
        else:
            return 2**31 - 1 if res >= 2**31 else res         
```
