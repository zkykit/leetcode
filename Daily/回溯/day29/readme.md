
### 491 递增子序列
### [题目链接](https://leetcode.cn/problems/non-decreasing-subsequences/submissions/)
### 思路：同层不可重复，以及不可在最开始排序(题目要求的)，
```
class Solution(object):
    def findSubsequences(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        result = []
        path = []
        self.backtracking(nums,0,path,result)
        return result
    

    def backtracking(self,nums,startIndex,path,result):
        if len(path)>1:
            result.append(path[:])
        used = set()
        for i in range(startIndex,len(nums)):
        #下一行不用 nums[i]<nums[i-1]是因为对 i 大小没有限制
            if(path and nums[i]<path[-1]) or nums[i] in used:
                continue
            
            used.add(nums[i])
            path.append(nums[i])
            self.backtracking(nums,i+1,path,result)
            path.pop()

```


### 45全排列
### [题目链接](https://leetcode.cn/problems/permutations/submissions/)
### 思路：首先排列是有序的，一个元素只用一次,注意这里的 used 如何初始化
```
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        result = []
        path = []
        self.backtracking(nums,path,result,[False]*len(nums))
        return result
    def backtracking(self,nums,path,result,used):
        if len(path) == len(nums):
            result.append(path[:])
            return
        for i in range(len(nums)):
            if used[i]:
                continue
            used[i] = True
            path.append(nums[i])
            self.backtracking(nums,path,result,used)
            path.pop()
            used[i] = False

```

### 全排列47
### [题目链接](https://leetcode.cn/problems/permutations-ii/submissions/)
### 思路：1.同层不重复需要 sort以及在 for 循环里加上判定条件而不是循环外 2. 注意我写过的判定条件，值得思考
### 复杂度： 时间和空间都是 n
```
class Solution(object):
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        path = []
        result = []
        nums.sort()
        self.backtracking(nums,path,result,[False]*len(nums))
        return result

    def backtracking(self,nums,path,result,used):
        if len(path) == len(nums):
            result.append(path[:])
            return

        for i in range(len(nums)):#判定条件写入 for loop
            if (i>0 and nums[i]==nums[i-1] and used[i-1]==False) or used[i] == True:
                continue
            
            used[i] = True
            path.append(nums[i])
            self.backtracking(nums,path,result,used)
            path.pop()
            used[i] = False
                
            

```