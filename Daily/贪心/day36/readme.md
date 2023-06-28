### 435无重叠区间
### [题目链接](https://leetcode.cn/problems/non-overlapping-intervals/submissions/)
### 思路：和前一天有点区别，注意大小符号以及 min何时使用，理解题意就好写了
```
class Solution(object):
    def eraseOverlapIntervals(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: int
        """
        if not intervals:
            return 0
        intervals.sort(key=lambda x:x[0])
        result=0
        for i in range(1,len(intervals)):
            if intervals[i-1][1]>intervals[i][0]:#发生重叠
                result+=1
                intervals[i][1] = min(intervals[i][1],intervals[i-1][1])
            
        return result

```