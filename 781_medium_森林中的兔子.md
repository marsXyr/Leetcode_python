# Leetcode 781 森林中的兔子
***
### 题目描述

森林中，每个兔子都有颜色。其中一些兔子（可能是全部）告诉你还有多少其他的兔子和自己有相同的颜色。我们将这些回答放在 `answers` 数组里。

返回森林中兔子的最少数量。


**示例:**

    示例:
	输入: answers = [1, 1, 2]
	输出: 5
	解释:
	两只回答了 "1" 的兔子可能有相同的颜色，设为红色。
	之后回答了 "2" 的兔子不会是红色，否则他们的回答会相互矛盾。
	设回答了 "2" 的兔子为蓝色。
	此外，森林中还应有另外 2 只蓝色兔子的回答没有包含在数组中。
	因此森林中兔子的最少数量是 5: 3 只回答的和 2 只没有回答的。

	输入: answers = [10, 10, 10]
	输出: 11

	输入: answers = []
	输出: 0
	
**说明：**

1. `answers` 的长度最大为`1000`。
2. `answers[i]` 是在 `[0, 999]` 范围内的整数。

### 考点

数学、哈希表


### 代码
执行用时: **64ms**, 内存消耗: **13.9MB**

```
class Solution:
    def numRabbits(self, answers: List[int]) -> int:
        res, dic = 0, dict()
        for answer in answers:
            if answer == 0 or str(answer) not in dic:
                res += answer + 1
                dic[str(answer)] = answer
            else:
                dic[str(answer)] -= 1
                if dic[str(answer)] == 0:
                    del(dic[str(answer)])
        return res
```

