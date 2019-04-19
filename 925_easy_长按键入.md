# Leetcode 925 长按键入
***
### 题目描述
你的朋友正在使用键盘输入他的名字 `name`。偶尔，在键入字符`c`时，按键可能会被*长按*，而字符可能被输入 1 次或多次。  

你将会检查键盘输入的字符`typed`。如果它对应的可能是你的朋友的名字（其中一些字符可能被长按），那么就返回 `True`。  

**示例1:**   
	
	输入：name = "alex", typed = "aaleex"
	输出：true
	解释：'alex' 中的 'a' 和 'e' 被长按。

**示例2:**   
	
	输入：name = "saeed", typed = "ssaaedd"
	输出：false
	解释：'e' 一定需要被键入两次，但在 typed 的输出中不是这样。
	
**示例3:**   
	
	输入：name = "leelee", typed = "lleeelee"
	输出：true

**示例4:**   
	
	输入：name = "laiden", typed = "laiden"
	输出：true
	解释：长按名字中的字符并不是必要的。
	
	
**提示**

* `name.length <= 1000`
* `typed.length <= 1000`
* `name` 和 `typed` 的字符都是小写字母。

### 考点

* 字符串操作


### 代码  
执行用时 **52ms**, 内存消耗 **13.1MB**

```
class Solution:
    def isLongPressedName(self, name: str, typed: str) -> bool:
        m, n = len(name), len(typed)
        i, j = 0, 0
        while j < n and i < m:
            if typed[j] == name[i]:
                i += 1
                j += 1
            else:
                j += 1
        return True if i == m else False          
```






	