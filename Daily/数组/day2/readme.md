# 代码随想录训练营第一天 | Leetcode 977 有序数组的平方，Leetcode 209 长度最小的子数组 Leetcode 59 螺旋矩阵

## 题目链接
[https://leetcode.cn/problems/squares-of-a-sorted-array/]

## 思路：
### 双指针，初始化之后，分别表示lm,rm，谁大谁替换到数组的最后一位，在循环的过程，left 和 right 指针向中心靠拢，条件允许 left=right

```
class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        result = [-1]*n
        left,right,k = 0,n-1,n-1
        while left<=right:
            lm = nums[left]**2
            rm = nums[right]**2
            if lm > rm:
                result[k] = lm
                left+=1
            else:
                result[k] = rm
                right-=1
            k-=1
        return result 
```
## 题目链接
[https://leetcode.cn/problems/minimum-size-subarray-sum/submissions/]
## 思路
### 重点是知道 subl是怎么写的以及while 的一个循环之后如何改变 sum
```
class Solution(object):
    def minSubArrayLen(self, target, nums):
        """
        :type target: int
        :type nums: List[int]
        :rtype: int
        """
        i = 0; sum = 0; result = float('inf')
        n = len(nums)
        for j in range(n):
            sum+=nums[j]
            while sum>=target:
                subl = j-i+1
                result = min(result,subl)
                sum-=nums[i]
                i+=1
        return 0 if result == float('inf') else result
```

## 题目链接
[https://leetcode.cn/problems/spiral-matrix-ii/submissions/]
## 思路
### 1. 变量的初始化 2. 对于行列变化要清晰 3. 最后判断一下奇数列或行的情况即可

```
class Solution(object):
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        nums = [[0]*n for _ in range(n)]
        count=1
        mid,loop = n//2,n//2
        startx,starty = 0,0
        for offset in range(1,loop+1):
            #行不变，列+1
            for i in range(starty,n-offset):
                nums[startx][i] = count; count+=1
            #列不变，行+1
            for i in range(startx,n-offset):
                nums[i][n-offset] = count; count+=1
            #行不变，列-1
            for i in range(n-offset,starty,-1):
                nums[n-offset][i] = count; count+=1
            #列不变，行-1
            for i in range(n-offset,startx,-1):
                nums[i][starty] = count; count+=1
            startx+=1
            starty+=1
        if n%2 == 1:
            nums[mid][mid] = count
        return nums
```