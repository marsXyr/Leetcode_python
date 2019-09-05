# Leetcode 692 前K个高频单词
***
### 题目描述

给一非空的单词列表，返回前 *k* 个出现次数最多的单词。

返回的答案应该按单词出现频率由高到低排序。如果不同的单词有相同出现频率，按字母顺序排序。


**示例1:**

	输入: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
	输出: ["i", "love"]
	解析: "i" 和 "love" 为出现次数最多的两个单词，均为2次。
    	注意，按字母顺序 "i" 在 "love" 之前。
    	
**示例2:**

	输入: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
	输出: ["the", "is", "sunny", "day"]
	解析: "the", "is", "sunny" 和 "day" 是出现次数最多的四个单词，
    	出现次数依次为 4, 3, 2 和 1 次。


**注意：**

1. 假定 *k* 总为有效值， 1 ≤ *k* ≤ 集合元素数。
2. 输入的单词均由小写字母组成。

**扩展：**

尝试以 *O(n log k)* 时间复杂度和 *O(n)* 空间复杂度解决。


### 考点

堆、字典树、哈希表


### 思路

#### 排序

算法： 

计算每个单词的频率，并使用使用这些频率的自定义排序关系对单词进行排序。然后取前 **k**。

复杂度分析： 

* 时间复杂度：O(N logN)。其中 N 是 words 的长度。我们用 O(N) 时间计算每个单词的频率，然后用 O(N logN) 时间对给定的单词进行排序。
* 空间复杂度：O(N)，用来存放答案的地方。

#### 堆

算法：

* 计算每个单词的频率，然后将其添加到存储到大小为 k 的小根堆中。它将频率最小的候选项放在堆的顶部。最后，我们从堆中弹出最多 k 次，并反转结果，就可以得到前 k 个高频单词。
* 在 Python 中，我们使用 heapq\heapify，它可以在线性时间内将列表转换为堆，从而简化了我们的工作。

复杂度分析：

* 时间复杂度：O(N logk)。其中 N 是 words 的长度。我们用 O(N) 的时间计算每个单词的频率，然后将 N 个单词添加到堆中，添加每个单词的时间为 O(log k) 。最后，我们从堆中弹出最多 k 次。因为 k ≤ N 的值，总共是 O(N logk)。
* 空间复杂度：O(N)，用于存储我们计数的空间。


### 代码1(排序)
执行用时: **88ms**, 内存消耗: **13.9MB**

```
class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        count = collections.Counter(words)
        words = count.keys()
        words.sort(key = lambda x: (-count[x], x))
        return words[:k]
```

### 代码2(堆)

```
class Solution(object):
    def topKFrequent(self, words, k):
        count = collections.Counter(words)
        heap = [(-freq, word) for word, freq in count.items()]
        heapq.heapify(heap)
        return [heapq.heappop(heap)[1] for _ in xrange(k)]
```


### 代码3(堆排序库)

```
class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
    	 from heapq import nsmallest
        return [x[1] for x in heapq.nsmallest(k, [(v, k) for k, v in collections.Counter(words).items()], key=lambda a: (-a[0], a[1]))]
```