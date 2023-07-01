
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

### 674最长连续递增子序列
### [题目链接](https://leetcode.cn/problems/longest-continuous-increasing-subsequence/submissions/)
### 思路：改变在于递推公式，不需要 j，直接用 i-1就完事儿
```
class Solution(object):
    def findLengthOfLCIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        result = 1
        dp = [1]*len(nums)

        for i in range(1,len(nums)):
            if nums[i-1]<nums[i]:
                dp[i] = dp[i-1]+1
            result = max(result,dp[i])
        return result
```



### 718最长重复子数组
### [题目链接](https://leetcode.cn/problems/maximum-length-of-repeated-subarray/submissions/)
### 思路：注意这里是二维，而且递推公式要注意，以及一般的初始化方式.
```
class Solution(object):
    def findLength(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: int
        """
        result = 0
        dp = [[0]*(len(nums2)+1) for _ in range(len(nums1)+1)]
        for i in range(1,len(nums1)+1):
            for j in range(1,len(nums2)+1):
                if nums1[i-1]==nums2[j-1]:
                    dp[i][j] = dp[i-1][j-1]+1
                result = max(result, dp[i][j])
        return result

```