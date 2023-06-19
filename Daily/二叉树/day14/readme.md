## 二叉树
### [题目链接](https://leetcode.cn/problems/binary-tree-preorder-traversal/submissions/)
### 思路：
#### 前序遍历：中左右，后序：左右中，中序：左中右
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root: return []
        left = self.preorderTraversal(root.left)
        right = self.preorderTraversal(root.right)

        return [root.val]+left+right
```