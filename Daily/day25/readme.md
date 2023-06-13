
### 216 组合总和
### [题目链接]()
### 思路：

```
class Solution(object):
    def combinationSum3(self, k, n):
        """
        :type k: int
        :type n: int
        :rtype: List[List[int]]
        """
        result = []
        self.backtracking(k,n,0,1,[],result)
        return result
    def backtracking(self,k,targetsum,currentsum,startIndex,path,result):
        if currentsum > targetsum:
            return
        if len(path) == k:
            if targetsum == currentsum:
                result.append(path[:])
            return
        
        for i in range(startIndex, 9-(k-len(path))+2):
            currentsum+=i
            path.append(i)
            self.backtracking(k,targetsum,currentsum,i+1,path,result)
            currentsum-=i
            path.pop()

```


### 17电话号码的字母组合
### [题目链接](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/submissions/)
### 思路：注意 for 循环都比较相似，先 append->递归->再回溯；注意这里用到的对于 letterMap 数据信息的提取
```
class Solution(object):
    def __init__(self):
        self.lettermap = [
        "",     # 0
        "",     # 1
        "abc",  # 2
        "def",  # 3
        "ghi",  # 4
        "jkl",  # 5
        "mno",  # 6
        "pqrs", # 7
        "tuv",  # 8
        "wxyz"  # 9
        ]
        self.result = []
        self.s = ""
    
    def backtracking(self,digits,index):
        if index == len(digits):
            self.result.append(self.s)
            return
        digit = int(digits[index])
        letters = self.lettermap[digit]
        for i in range(len(letters)):
            self.s +=letters[i]
            self.backtracking(digits,index+1)
            self.s = self.s[:-1]


    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if not len(digits): return self.result
        self.backtracking(digits,0)
        return self.result
    
    
```