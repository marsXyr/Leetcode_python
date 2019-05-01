# Leetcode 322 零钱兑换
***
### 题目描述
给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 `-1`。


**示例1:**

	输入: coins = [1, 2, 5], amount = 11
	输出: 3 
	解释: 11 = 5 + 5 + 1
 

**示例2:**

	输入: coins = [2], amount = 3
	输出: -1
	

### 考点

* DFS / BFS / 动态规划


### 代码(动态规划)  
执行用时: **1940ms**, 内存消耗: **13MB** 


```
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] * (amount + 1)
        dp[0] = 0
        for i in range(1, amount + 1):
            for coin in coins:
                if i - coin >= 0:
                    dp[i] = min(dp[i], dp[i-coin]+1)
        return dp[-1] if dp[-1] != float('inf') else -1
```

### 代码2（dfs+字典）

```
class Solution:
        def coinChange(self, coins: 'List[int]', amount: 'int') -> 'int':
        	  from collections import defaultdict
            lookup = defaultdict(int)
            if amount < 1:
                return 0
    
            def helper(amount):
                if amount < 0:
                    return -1
                if amount == 0:
                    return 0
                if lookup[amount]:
                    return lookup[amount]
                min_num = 2 ** 31 - 1
                for coin in coins:
                    res = helper(amount - coin)
                    # min_num = min(min_num,res + 1)
                    if res >= 0 and res < min_num:
                        min_num = res + 1
                lookup[amount] = min_num if min_num != 2 ** 31 - 1 else -1
                return lookup[amount]
    
            return helper(amount)
```

### 代码3（dfs+约束）

```
class Solution:
        def coinChange(self, coins: 'List[int]', amount: 'int') -> 'int':
            self.res = float("inf")
            n = len(coins)
            if amount == 0:
                return 0
            coins.sort(reverse=True)
            if amount < coins[-1]:
                return -1
    
            def dfs(loc, remain, count):
                if remain == 0:
                    self.res = min(self.res, count)
                else:
                    for i in range(loc, n):
                        if coins[i] <= remain < coins[i] * (self.res - count):
                            dfs(i, remain - coins[i], count + 1)
    
            for i in range(n):
                dfs(i, amount, 0)
            return self.res if self.res != float("inf") else -1
```

### 代码4（bfs）

```
class Solution:
        def coinChange(self, coins: 'List[int]', amount: 'int') -> 'int':
            res = 0
            cur = [0]
            visited = set()
            coins.sort()
            while cur:
                next_time = []
                res += 1
                for tmp in cur:
                    for coin in coins:
                        sum_num = tmp + coin
                        if sum_num == amount:
                            return res
                        elif sum_num > amount:
                            break
                        elif sum_num < amount and sum_num not in visited:
                            next_time.append(sum_num)
                            visited.add(sum_num)
                cur = next_time
            return -1 if amount else 0
```

### 大佬做法
```
import math
class Solution:
    def coinChange(self, coins, amount):
        coins.sort(reverse=True)
        len_coins, result = len(coins), amount+1

        def countCoins(index, target, count):
            nonlocal result
            if count + math.ceil(target/coins[index]) >= result:
                return 

            if target % coins[index] == 0:
                result = count + target//coins[index]
                return

            if index == len_coins - 1:
                return

            for i in range(target//coins[index], -1, -1):
                countCoins(index+1, target - coins[index]*i, count+i)

        countCoins(0, amount, 0)
        return -1 if result > amount else result
```






	