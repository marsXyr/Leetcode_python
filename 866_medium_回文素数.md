# Leetcode 866 回文素数
***
### 题目描述
求出大于或等于 `N` 的最小回文素数。

回顾一下，如果一个数大于 1，且其因数只有 1 和它自身，那么这个数是素数。

例如，2，3，5，7，11 以及 13 是素数。

回顾一下，如果一个数从左往右读与从右往左读是一样的，那么这个数是回文数。

例如，12321 是回文数。


**示例1:**   

	输入：6
	输出：7
	
**示例2:**   

	输入：8
	输出：11
	
**示例3:**   

	输入：13
	输出：101

	
**提示:** 

* `1 <= N <= 10^8`
* 答案肯定存在，且小于 `2 * 10^8`



### 考点

数学

### 思路
偶数位的回文数除了11都是质数，比如N=1001，下一次遍历可以从N=10001开始，这样的话9989900这个用例不会超时



### 代码1
执行用时: **368ms**, 内存消耗: **13.8MB**

```
class Solution:
    def primePalindrome(self, N: int) -> int:

        def isPrime(num):
            for i in range(2, int(num ** 0.5) + 1):
                if num % i == 0:
                    return False
            return True if num > 1 else False
        
        def isPalindrome(num):
            return str(num) == str(num)[::-1]
        
        while True:
            if isPalindrome(N) and isPrime(N):
                return N
            else:
                if N > 11 and len(str(N)) % 2 == 0:
                    N = 10 ** len(str(N)) + 1
                else:
                    N += 1
```

### 代码2(执行时间：52ms)

```
class Solution(object):
    def primePalindrome(self, N):
        """
        :type N: int
        :rtype: int
        """
        def judge_pri(n):
            if (n+1)%6!=0 and (n-1)%6!=0:
                return False
            left,right = 2,n//2
            while left <=right:
                if n%left == 0:
                    return False
                else:
                    left += 1
                    right = n//left
            return True
        def find_pal(num):
            res = str(num)
            n = len(res)//2
            if res[n-1::-1] >= res[n+1:]:
                return int(res[:n+1]+res[n-1::-1])
            else:
                if res[n]!='9':
                    t = str(int(res[n])+1)
                    return int(res[:n]+t+res[n-1::-1])
                else:
                    a = str(int(res[:n])+1)
                    if len(a)>n:
                        return 10*(2*n+1)+1
                    else:
                        return int(a+'0'+a[::-1])
        if N == 1:
            return 2
        elif N < 4:
            return N
        elif N < 6:
            return 5
        elif N < 8:
            return 7
        elif N < 12:
            return 11
        K = len(str(N))
        if K % 2 == 0:
            return self.primePalindrome(10 ** K + 1)
        else:
            res = find_pal(N)
            if judge_pri(res):
                return res
            else:
                return self.primePalindrome(res + 1)
```