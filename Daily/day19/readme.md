### 654 最大二叉树
### [题目链接](https://leetcode.cn/problems/maximum-binary-tree/submissions/)
### 使用跟105106相似的思想，
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
import numpy as np
class Solution(object):
    def constructMaximumBinaryTree(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if not nums:
            return None
        #确定分割数的索引及填入 root
        root_val = np.max(nums)
        root = TreeNode(root_val)
        separate_index = nums.index(root.val)
        #分割前序
        preorder_left =  nums[:separate_index]
        preorder_right = nums[separate_index+1:]
        #递归
        root.left = self.constructMaximumBinaryTree(preorder_left)
        root.right = self.constructMaximumBinaryTree(preorder_right)
        return root   

```


### 617 合并二叉树
### [题目链接](https://leetcode.cn/problems/merge-two-binary-trees/submissions/)
### 思路 : 
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def mergeTrees(self, root1, root2):
        """
        :type root1: TreeNode
        :type root2: TreeNode
        :rtype: TreeNode
        """
        if root1 is None: return root2
        if root2 is None: return root1

        root1.val+=root2.val
        root1.left = self.mergeTrees(root1.left,root2.left)
        root1.right = self.mergeTrees(root1.right,root2.right)
        return root1
```


### 700 二叉树中的搜索
### [题目链接](https://leetcode.cn/problems/search-in-a-binary-search-tree/submissions/)
### 思路：
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def searchBST(self, root, val):
        """
        :type root: TreeNode
        :type val: int
        :rtype: TreeNode
        """
        if not root or root.val == val:
            return root
        if root.val > val:
            return self.searchBST(root.left,val)
        if root.val < val:
            return self.searchBST(root.right,val)

```


### 98验证二叉搜索树
### [题目链接](https://leetcode.cn/problems/validate-binary-search-tree/submissions/)
### 思路：使用中序遍历，注意写法和要求左小右大的顺序
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def __init__(self):
        self.maxValue = float('-inf')
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root is None:
            return True
        left = self.isValidBST(root.left)
        #中
        if self.maxValue < root.val:
            self.maxValue = root.val
        else:
            return False
        right = self.isValidBST(root.right)

        return left and right
        
```