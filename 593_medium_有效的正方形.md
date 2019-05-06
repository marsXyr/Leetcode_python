# Leetcode 593 有效的正方形
***
### 题目描述
给定二维空间中四点的坐标，返回四点是否可以构造一个正方形。

一个点的坐标（x，y）由一个有两个整数的整数数组表示。


**示例：**   
	
	输入: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]
	输出: True

    	
**注意：**  

1. 所有输入整数都在 [-10000，10000] 范围内。
2. 一个有效的正方形有四个等长的正长和四个等角（90度角）。
3. 输入点没有顺序。
	

### 考点

* 数学

### 思路
首先想到的是判断正方形的条件是：四条边相等且对角线相等，但是因为整数范围是10000，乘积开方运算比较费时，所以采用四点坐标的关系来判断。（代码稍长，懒得优化长度）


### 代码  
执行用时: **56ms**, 内存消耗: **12.9MB** 

```
class Solution:
    def validSquare(self, p1: List[int], p2: List[int], p3: List[int], p4: List[int]) -> bool:
        x = sorted([p1[0], p2[0], p3[0], p4[0]])
        y = sorted([p1[1], p2[1], p3[1], p4[1]])
        # 判断是否是点或线
        if x[0] == x[3] or y[0] == y[3]:
            return False
        # 如果正方形是垂直于坐标轴的（也就是有两个点横坐标相同）
        if x[0] == x[1]:
            if (x[2] == x[3]) and (y[0] == y[1]) and (y[2] == y[3]) and (x[2]-x[1] == y[2]-y[1]):
                return True
            else:
                return False
        # 正方形不垂直于坐标轴
        else:
            # 左边的点
            if x[0] == p1[0]:
                left = p1
            elif x[0] == p2[0]:
                left = p2
            elif x[0] == p3[0]:
                left = p3
            else:
                left = p4
            # 右边的点
            if x[3] == p1[0]:
                right = p1
            elif x[3] == p2[0]:
                right = p2
            elif x[3] == p3[0]:
                right = p3
            else:
                right = p4
            # 下边的点
            if y[0] == p1[1]:
                down = p1
            elif y[0] == p2[1]:
                down = p2
            elif y[0] == p3[1]:
                down = p3
            else:
                down = p4
            # 上边的点
            if y[3] == p1[1]:
                up = p1
            elif y[3] == p2[1]:
                up = p2
            elif y[3] == p3[1]:
                up = p3
            else:
                up = p4
            # 判断条件
            if (right[0] + left[0] == up[0] + down[0]) and (right[1] + left[1] == up[1] + down[1]) and (down[0] - left[0] == right[1] - down[1]):
                return True 
            else:
                return False
```

### 代码'   
下面给出乘积运算代码

```
class Solution:
    def validSquare(self, p1, p2, p3, p4):
        """
        :type p1: List[int]
        :type p2: List[int]
        :type p3: List[int]
        :type p4: List[int]
        :rtype: bool
        """
        p1, p2, p3, p4 = sorted((p1, p2, p3, p4))
        x1,y1=p2[0]-p1[0],p2[1]-p1[1]
        x2,y2=p3[0]-p1[0],p3[1]-p1[1]
        x3,y3=p4[0]-p1[0],p4[1]-p1[1]

        return x1+x2==x3 and y1+y2==y3 and x1*x2+y1*y2==0 and x1**2+y1**2==x2**2+y2**2 !=0
```









	
