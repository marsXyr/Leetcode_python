# Leetcode 676 实现一个魔法字典
***
### 题目描述

实现一个带有`buildDict`, 以及 `search`方法的魔法字典。

对于`buildDict`方法，你将被给定一串不重复的单词来构建一个字典。

对于`search`方法，你将被给定一个单词，并且判定能否只将这个单词中一个字母换成另一个字母，使得所形成的新单词存在于你构建的字典中。


**示例1:**

    Input: buildDict(["hello", "leetcode"]), Output: Null
	Input: search("hello"), Output: False
	Input: search("hhllo"), Output: True
	Input: search("hell"), Output: False
	Input: search("leetcoded"), Output: False

	
**注意：**

1. 你可以假设所有输入都是小写字母 `a-z`。
2. 为了便于竞赛，测试所用的数据量很小。你可以在竞赛结束后，考虑更高效的算法。
3. 请记住**重置**MagicDictionary类中声明的类变量，因为静态/类变量会在多个测试用例中保留。

### 考点

哈希表

### 思路

* 如果一个字符中只有一个字符可以更改，则他们的汉明距离为1。
* 在搜索新单词时，我们只检查长度相同的单词。


### 代码
执行用时: **32ms**, 内存消耗: **13.7MB**

```
class MagicDictionary:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.dic = collections.defaultdict(list)
        

    def buildDict(self, dict: List[str]) -> None:
        """
        Build a dictionary through a list of words
        """
        for word in dict:
            self.dic[len(word)].append(word)
        

    def search(self, word: str) -> bool:
        """
        Returns if there is any word in the trie that equals to the given word after modifying exactly one character
        """
        return any(sum(a != b for a, b in zip(word, cand)) == 1 for cand in self.dic[len(word)])
        


# Your MagicDictionary object will be instantiated and called as such:
# obj = MagicDictionary()
# obj.buildDict(dict)
# param_2 = obj.search(word)
```
