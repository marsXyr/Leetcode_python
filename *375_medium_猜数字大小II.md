# Leetcode 375 猜数字大小 II
***
### 题目描述

我们正在玩一个猜数游戏，游戏规则如下：

我从 **1** 到 **n** 之间选择一个数字，你来猜我选了哪个数字。

每次你猜错了，我都会告诉你，我选的数字比你的大了或者小了。

然而，当你猜了数字 x 并且猜错了的时候，你需要支付金额为 x 的现金。直到你猜到我选的数字，你才算赢得了这个游戏。

**示例1:**  

	n = 10, 我选择了8.

	第一轮: 你猜我选择的数字是5，我会告诉你，我的数字更大一些，然后你需要支付5块。
	第二轮: 你猜是7，我告诉你，我的数字更大一些，你支付7块。
	第三轮: 你猜是9，我告诉你，我的数字更小一些，你支付9块。

	游戏结束。8 就是我选的数字。

	你最终要支付 5 + 7 + 9 = 21 块钱。
	
给定 **n ≥ 1**，计算你至少需要拥有多少现金才能确保你能赢得这个游戏。

### 考点

动态规划、极小极大值

### 思路
`dp[j][i]`表示从`[j,i]`中猜出正确数字所需要的最少花费金额.(`dp[i][i] = 0`)
        假设在范围`[j,i]`中选择k, 则选择k的最少花费金额为: `max(dp[j][k-1], dp[k+1][i]) + k`
        用max的原因是我们要计算最坏反馈情况下的最少花费金额(选了`k`之后, 正确数字落在花费更高的那侧)        

### 代码
执行用时: **932ms**, 内存消耗: **13.6MB**。

```
class Solution:
    def getMoneyAmount(self, n: int) -> int:
        dp = [[0] * (n + 1) for _ in range(n + 1)]
        for i in range(2, n+1):
            for j in range(i-1, 0, -1):
                global_min = float('inf')               
                for k in range(j, i):
                    global_min = min(global_min, k + max(dp[j][k-1], dp[k+1][i]))
                dp[j][i] = global_min
                        
        return dp[1][n]
```


### 代码2(大佬做法，执行时间: 112ms)

```
class Solution:
    def getMoneyAmount(self, n):
        def findmin(m, n, dic={}):
            if (m,n) in dic:
                return dic[(m,n)]
            if m==n:
                dic[(m,n)] = 0
                return 0
            if n==m+1:
                dic[(m,n)] = m
                return m
            result = (m+n)*(n-m+1)/2        # m到n的和
            for i in range(m+53*(n-m)//100,n):  # ？？？
                boolen = False
                if findmin(m,i-1,dic)>findmin(i+1,n,dic):
                    temp = findmin(m,i-1,dic)+i
                    boolen = True
                else:
                    temp = findmin(i+1,n,dic)+i
                if temp<result:
                    result = temp
                if boolen:
                    break
            dic[(m,n)]=result
            return result
        return  findmin(1,n)
```



