### 78子集 
### [题目链接](https://leetcode.cn/problems/subsets/submissions/)
### 思路：回溯算法，和之前的回溯没有什么区别
```
class Solution(object):
    def __init__(self):
        self.result = []
        self.path = []
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        self.backtracking(nums,[],self.result,0)
        return self.result

    def backtracking(self,nums,path,result,startIndex):
        result.append(path[:])
        if startIndex>=len(nums):
            return  
        for i in range(startIndex,len(nums)):
            path.append(nums[i])
            self.backtracking(nums,path,result,i+1)
            path.pop()
```