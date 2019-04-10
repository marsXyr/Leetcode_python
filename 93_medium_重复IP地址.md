# Leetcode 93.复制IP地址
***
### 题目描述
给定一个只包含数字的字符串，复原它并返回所有可能的IP地址格式。  

**示例:**   
	
	输入：“25525511135”
	输出：["255.255.111.35", "255.255.11.35"]
	
	
### 关键点  

* 每个IP段的范围是0-255，某段不是1位时，第一位数字不能为0
* 对整个序列求解，而非子集。序列顺序不能改变。


### 考点

* 回溯法DFS


### 代码  
执行用时 **56ms**, 内存消耗 **13.1MB**

```
class Solution:
    
    def BackTrace(self, part, s, ips, res):
    	"""
    	part: 用逗号分隔开的part数量，从左到右一共分为4部分
    	s: 剩余待分的字符串
    	ips: 已划分的部分 [[part1], [part2], ...]
    	res: 存放结果
    	"""
        if not s:  # 如果s为None
            if part == 4:
                res.append('.'.join(ips))
            return
        if part == 4:
            return
        
        # 1 位
        self.BackTrace(part+1, s[1:], ips+[s[:1]], res)
        # 2 位及以上
        if s[0] != '0':
            if len(s) >= 2:
                self.BackTrace(part+1, s[2:], ips+[s[:2]], res)
            if (len(s) >= 3) and (int(s[:3]) <= 255):
                self.BackTrace(part+1, s[3:], ips+[s[:3]], res) 
    
    def restoreIpAddresses(self, s: str) -> List[str]:
        
        results = []
        self.BackTrace(0, s, [], results)
        return results
```


	