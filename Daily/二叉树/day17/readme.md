
### 110 平衡二叉树 递归法,自我调用
### [题目链接](https://leetcode.cn/problems/balanced-binary-tree/)
### 思路：建立新函数计算高度，其中包括分别左右的高度

```

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.get_height(root) != -1
    def get_height(self,node):
        if not node: return 0
        left = self.get_height(node.left)
        right = self.get_height(node.right)
        if left == -1 or right == -1 or abs(left-right)>1:
            return -1
        return max(left,right)+1
       
```

### 257 二叉树的所有路径 
### [题目链接](https://leetcode.cn/problems/binary-tree-paths/)
### 思路:递归+回溯
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def binaryTreePaths(self, root):
        """
        :type root: TreeNode
        :rtype: List[str]
        """
        path = []
        result = []
        self.traversal(root,path,result)
        return result
    def traversal(self,cur,path,result):
        path.append(cur.val)
        if not cur.left and not cur.right:
            sPath = '->'.join(map(str,path))
            result.append(sPath)
            return 
        if cur.left:
            self.traversal(cur.left,path,result)
            path.pop()#回溯
        if cur.right:
            self.traversal(cur.right,path,result)
            path.pop()
    
```
### 404 左叶子之和
### [题目链接](https://leetcode.cn/problems/sum-of-left-leaves/)
### 思路：因为只要是右子树的左节点就一定是叶节点,所以只对左子树后面加 if 
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def sumOfLeftLeaves(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        if root.left == None and root.right == None:
            return 0
        leftvalue = self.sumOfLeftLeaves(root.left)
        if root.left and not root.left.left and not root.left.right:
            leftvalue = root.left.val
        rightvalue = self.sumOfLeftLeaves(root.right)
        return leftvalue+rightvalue

```