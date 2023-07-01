
### 300最长递增子序列
### [题目链接](https://leetcode.cn/problems/longest-increasing-subsequence/submissions/)
### 思路：![image]()
### 重点是dp 的初始化以及推导公式，推导公式见上图
```
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 1:
            return 1
        result = 0
        dp = [1]*len(nums)
        for i in range(1,len(nums)):
            for j in range(0,i):
                if nums[j]<nums[i]:
                    dp[i] = max(dp[i],dp[j]+1)
            result = max(result, dp[i])
        return result
```