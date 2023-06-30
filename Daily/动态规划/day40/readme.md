

### 343整数拆分
### [题目链接](https://leetcode.cn/problems/integer-break/submissions/)
### 思路：注意 for 是从3开始，以及拆分出来的数不超过 i//2+1
```
class Solution(object):
    def integerBreak(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp = [0]*(n+1)
        dp[2] = 1
        for i in range(2,n+1):
            for j in range(1,i//2+1):
                dp[i] = max(dp[i],max((i-j)*j,dp[i-j]*j))

        return dp[n]
```
### 96不同的二叉搜索树
### [题目链接](https://leetcode.cn/problems/unique-binary-search-trees/submissions/)
### 思路：元素1为头结点搜索树的数量 = 右子树有2个元素的搜索树数量 * 左子树有0个元素的搜索树数量;元素2为头结点搜索树的数量 = 右子树有1个元素的搜索树数量 * 左子树有1个元素的搜索树数量;元素3为头结点搜索树的数量 = 右子树有0个元素的搜索树数量 * 左子树有2个元素的搜索树数量;  dp[3] = dp[2] * dp[0] + dp[1] * dp[1] + dp[0] * dp[2]
```
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp=[0]*(n+1)
        dp[0] = 1
        for i in range(1,n+1):
            for j in range(1,i+1):
                dp[i] += dp[j-1]*dp[i-j]
        return dp[n]
```