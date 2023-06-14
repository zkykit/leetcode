### 39 组合总和(可重复选择)
### [题目链接](https://leetcode.cn/problems/combination-sum/submissions/)
### 思路：注意可重复选择对于i 不需要+1
```
class Solution(object):
    def backtracking(self, candidates, target, sum, startIndex, path, result):
        if sum>target:
            return
        if sum == target:
            result.append(path[:])
            return result
        for i in range(startIndex, len(candidates)):
            path.append(candidates[i])
            sum += candidates[i]
            self.backtracking(candidates,target,sum,i,path,result)
            sum -= candidates[i]
            path.pop()

    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        result = []
        self.backtracking(candidates,target,0,0,[],result)
        return result

```


### 40组合总和
### [题目链接](https://leetcode.cn/problems/combination-sum-ii/submissions/)
### 思路：注意 for 循环的 if 条件,该算法通过回溯的方式遍历所有可能的组合，并根据条件进行剪枝，以提高效率。最终返回符合条件的组合结果列表。
```
class Solution(object):
    def backtracking(self, candidates, target, sum, startIndex, path, result):
        if sum == target:
            result.append(path[:])
            return
        for i in range(startIndex,len(candidates)):
            if i>startIndex and candidates[i]==candidates[i-1]:
                continue
            if sum + candidates[i]>target:
                break
            sum+=candidates[i]
            path.append(candidates[i])
            #进入下个分支
            self.backtracking(candidates,target,sum,i+1,path,result)
            sum-=candidates[i]
            path.pop()

    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        result = []
        candidates.sort()
        self.backtracking(candidates,target,0,0,[],result)
        return result
        
```

### 131分割回文串
### [题目链接](https://leetcode.cn/problems/palindrome-partitioning/submissions/)
### 思路：终止条件的确定，回文条件的确定即正反相等，记得最后 path.pop()
```
class Solution(object):
    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        result = []
        self.backtracking(s,0,[],result)
        return result
    def backtracking(self,s, startIndex, path, result):
        if startIndex == len(s):
            result.append(path[:])
            return
        for i in range(startIndex,len(s)):
            if s[startIndex:i+1] == s[startIndex:i+1][::-1]:
                path.append(s[startIndex:i+1])
                self.backtracking(s,i+1,path,result)
                path.pop()
            
```