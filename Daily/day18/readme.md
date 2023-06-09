### 514 找树左下角的值(最大深度的)
### [题目链接](https://leetcode.cn/problems/find-bottom-left-tree-value/submissions/)
### 思路：参数的初始化重要；


```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def findBottomLeftValue(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.max_depth = float('-inf')
        self.result = None
        self.traversal(root,0)
        return self.result

    def traversal(self,node,depth):
        if node.left is None and node.right is None:
            if depth>self.max_depth:
                self.max_depth = depth
                self.result = node.val
        if node.left:
            depth+=1
            self.traversal(node.left,depth)
            depth-=1
        if node.right:
            depth+=1
            self.traversal(node.right,depth)
            depth-=1


```

### 112 路径总和
### [题目链接](https://leetcode.cn/problems/path-sum/)
### 思路：还是要注意回溯回来；
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def hasPathSum(self, root, targetSum):
        """
        :type root: TreeNode
        :type targetSum: int
        :rtype: bool
        """
        if root is None:
            return False
        return self.traversal(root,targetSum-root.val)

    
    def traversal(self,node,count):
        if node.left is None and node.right is None and count ==0:
            return True
        if node.left is None and node.right is None and count !=0:
            return False
        if node.left:
            count -= node.left.val
            if self.traversal(node.left,count): return True
            count += node.left.val
        if node.right:
            count -= node.right.val
            if self.traversal(node.right,count): return True
            count += node.right.val
        return False
        
```

### 从中序与后序遍历序列构造二叉树 
### [题目链接](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
### 思路：见下题
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        if not postorder:
            return None
        root_val = postorder[-1]
        root = TreeNode(root_val)
        #找切割点_下标_中序
        separate_index = inorder.index(root_val)
        #切割中序数组
        inorder_left = inorder[:separate_index]
        inorder_right = inorder[separate_index+1:]
        #切割后序数组
        postorder_left = postorder[:len(inorder_left)]
        postorder_right = postorder[len(inorder_left):len(postorder)-1]
        #递归
        root.left = self.buildTree(inorder_left, postorder_left)
        root.right = self.buildTree(inorder_right, postorder_right)
        return root
```

### 从中序与后序遍历序列构造二叉树 
### [题目链接](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/submissions/)
### 思路见此图![image]()

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if not preorder:
            return None
        root_val = preorder[0]
        root = TreeNode(root_val)
        #找切割点_index_中序
        separate_index = inorder.index(root_val)
        #切中序
        inorder_left = inorder[:separate_index]
        inorder_right = inorder[separate_index+1:]
        #切前序
        preorder_left = preorder[1:1+len(inorder_left)]
        preorder_right = preorder[1+len(inorder_left):]
        #递归
        root.left = self.buildTree(preorder_left,inorder_left)
        root.right = self.buildTree(preorder_right,inorder_right)
        return root
```