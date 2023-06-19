
### 455分发饼干 (大饼干优先，倒序)
### [题目链接](https://leetcode.cn/problems/assign-cookies/submissions/)
### 思路: [image]()

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