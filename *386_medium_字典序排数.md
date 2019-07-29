# Leetcode 386 字典序排数
***
### 题目描述
给定一个整数 n, 返回从 1 到 n 的字典顺序。

例如，

给定 n =1 3，返回 [1,10,11,12,13,2,3,4,5,6,7,8,9] 。

请尽可能的优化算法的时间复杂度和空间复杂度。 输入的数据 n 小于等于 5,000,000。



### 考点

递归


### 代码(递归)
执行用时: **152ms**, 内存消耗: **19.4MB**

```
class Solution:
    def lexicalOrder(self, n: int) -> List[int]:
        res = []
        for i in range(1, 10):
            self.getNum(i, n, res)
        return res
    
    def getNum(self, i, n, res):
        if i <= n:
            res.append(i)
            cur = i * 10
            if cur <= n:
                for j in range(10):
                    self.getNum(cur + j, n, res)
```

### 代码(简洁写法)

```
class Solution:
    def lexicalOrder(self, n: int) -> List[int]:
        return sorted(range(1, n+1), key=lambda x: str(x))
```
