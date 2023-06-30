
### 198打家劫舍
### [题目链接](https://leetcode.cn/problems/house-robber/submissions/)
### 思路：返回 dp[-1]，即截止到最后一个房屋时的最大偷窃价值。
```
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)==0:
            return 0
        if len(nums)==1:
            return nums[0]
        
        dp = [0]*(len(nums))
        dp[0] = nums[0]
        dp[1] = max(nums[0],nums[1])
        for i in range(2,len(nums)):
            dp[i] = max(dp[i-1],dp[i-2]+nums[i])
        return dp[-1]
```

### 打家劫舍2
```
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        if len(nums) == 1:
            return nums[0]
        
        result1 = self.robRange(nums, 0, len(nums) - 2)  # 情况二
        result2 = self.robRange(nums, 1, len(nums) - 1)  # 情况三
        return max(result1, result2)
    # 198.打家劫舍的逻辑
    def robRange(self, nums: List[int], start: int, end: int) -> int:
        if end == start:
            return nums[start]
        
        prev_max = nums[start]
        curr_max = max(nums[start], nums[start + 1])
        
        for i in range(start + 2, end + 1):
            temp = curr_max
            curr_max = max(prev_max + nums[i], curr_max)
            prev_max = temp
        
        return curr_max
```

### 337打家劫舍3
### [题目链接](https://leetcode.cn/problems/house-robber-iii/submissions/)
### 思路：val_0 表示不偷当前节点，因此取左子树和右子树的最大值，并加上对应子树中选择偷取或不偷取的最大金钱。;val_1 表示偷当前节点，因此将当前节点的值加上左子树和右子树不偷取节点的最大金钱。

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        dp=self.traversal(root)
        return max(dp)
    def traversal(self,node):
        if not node:
            return (0,0)
        left = self.traversal(node.left)
        right = self.traversal(node.right)
        val_0 = max(left[0],left[1])+max(right[0],right[1])#不偷当前节点
        val_1 = node.val+left[0]+right[0]#偷当前节点
        return (val_0,val_1)
```