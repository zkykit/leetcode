### 455分发饼干 (大饼干优先，倒序)
### [题目链接](https://leetcode.cn/problems/assign-cookies/submissions/)
### 思路:见图片![image]()

```
class Solution(object):
    def findContentChildren(self, g, s):
        """
        :type g: List[int]
        :type s: List[int]
        :rtype: int
        """
        g.sort()
        s.sort()
        result = 0
        index = len(s)-1
        for i in range(len(g)-1,-1,-1):
            if index>=0 and s[index]>=g[i]:
                result+=1
                index-=1
            
        return result
```

### 376摆动序列
### [题目链接](https://leetcode.cn/problems/wiggle-subsequence/submissions/)
### 思路：通过设置 prediff 和 curdiff的大小关系来决定前后是否符合摆动，也就是一大一小一大一小
```
class Solution(object):
    def wiggleMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)<=1:
            return len(nums)
        result = 1
        prediff,curdiff = 0,0
        for i in range(len(nums)-1):
            curdiff = nums[i+1]-nums[i]
            if (prediff <= 0 and curdiff >0) or (prediff >= 0 and curdiff <0):
                result+=1
                prediff = curdiff
        return result
```

### 53最大子数组和
### [题目链接](https://leetcode.cn/problems/maximum-subarray/submissions/)
### 思路：for 循环 里面的判定条件重要
```
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        result = float('-inf')
        count = 0
        for i in range(len(nums)):
            count+=nums[i]
            if count>result:#取区间累积的最大值
                result = count
            if count<0: #重置最大子序起始位置
                count = 0
        return result

```