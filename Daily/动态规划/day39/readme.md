



### 62不同路径
### [题目链接](https://docs.qq.com/doc/DUE55cVJ5WkNoREhS?u=951c4665e8e14a3d9d538e3d44f93cc2)
### 思路：注意初始化，以及dp 公式，重要还是要理解公式怎么来的。，自己不容易想到
```
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        dp = [[0]*n for _ in range(m)]
        for i in range(m):
            dp[i][0]=1
        for j in range(n):
            dp[0][j]=1
        
        for i in range(1,m):
            for j in range(1,n):
                dp[i][j] = dp[i-1][j]+dp[i][j-1]
        return dp[m-1][n-1]
```


### 63不同路径
### [题目链接](https://leetcode.cn/problems/unique-paths-ii/submissions/)
### 思路：如果遇到障碍物，则跳出循环，后面的位置都默认为0;如果该位置不是障碍物，则将dp[0][j]设为1;使用两个嵌套的循环遍历除了第一行和第一列之外的其他位置
```
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        m=len(obstacleGrid)
        n=len(obstacleGrid[0])
        #如果障碍物在起点或终点
        if obstacleGrid[m-1][n-1] == 1 or obstacleGrid[0][0] == 1:
            return 0
        dp=[[0]*n for _ in range(m)]
        for i in range(m):
            if obstacleGrid[i][0] == 0:
                dp[i][0] = 1
            else:
                break
        for j in range(n):
            if obstacleGrid[0][j] == 0:
                dp[0][j] = 1
            else:
                break
        for i in range(1,m):
            for j in range(1,n):
                if obstacleGrid[i][j]==1:continue
                dp[i][j] = dp[i-1][j]+dp[i][j-1]
        return dp[m-1][n-1]

```