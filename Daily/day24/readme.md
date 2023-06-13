### 77组合
### [题目链接](https://leetcode.cn/problems/combinations/)
### 思路：startIndex 就是防止出现重复的组合,需要startIndex来记录下一层递归，搜索的起始位置
```
class Solution(object):
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        result = []
        self.backtracking(n,k,1,[],result)
        return result
    def backtracking(self, n,k,startIndex, path, result):
        if len(path) == k:
            result.append(path[:])
            return result
        for i in range(startIndex, n+1):
            path.append(i)
            self.backtracking(n,k,i+1,path,result)
            path.pop()

```