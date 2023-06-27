
### 860 柠檬水找零
### [题目链接](https://leetcode.cn/problems/lemonade-change/submissions/)
### 思路：注意这里对于取值不可以用 not，用大于小于号；还有就是重点是分情况讨论，只把 return False 的情况列出来，最后输出 True
```
class Solution(object):
    def lemonadeChange(self, bills):
        """
        :type bills: List[int]
        :rtype: bool
        """
        five,ten,twenty = 0,0,0
        for bill in bills:
            if bill is 5:
                five+=1
            if bill is 10:
                if five<=0:
                    return False
                five-=1
                ten+=1
            if bill is 20:
                if ten>0 and five>0:
                    ten-=1
                    five-=1
                elif five>=3:
                    five-=3
                else:
                    return False

        return True
```

### 452用最少数量的箭引爆气球
### [题目链接](https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/)
### 思路：注意需要排序,见图片
### ![image]()
```
class Solution(object):
    def findMinArrowShots(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        if not points:
            return 0
        points.sort(key=lambda x:x[0])
        result = 1
        for i in range(len(points)):
            if points[i-1][1]<points[i][0]:
                result+=1
            else:
                points[i][1] = min(points[i][1],points[i-1][1])
        return result
```

