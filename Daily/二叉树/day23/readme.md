

### 108 将有序数组转换为二叉搜索树
### [题目链接](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/submissions/)
### 思路：本质就是寻找分割点，分割点作为当前节点，然后递归左区间和右区间。
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def traversal(self,nums,left,right):
        if left>right:
            return None
        
        mid = (left+right)//2
        root = TreeNode(nums[mid])
        root.left = self.traversal(nums,left,mid-1)
        root.right = self.traversal(nums,mid+1,right)
        return root


    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        root = self.traversal(nums,0,len(nums)-1)
        return root
         

```