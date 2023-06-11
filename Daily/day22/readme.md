### 二叉搜索树的最近公共祖先
### [题目链接]()
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def traversal(self,cur,p,q):
        if not cur:
            return None
        if cur.val > p.val and cur.val > q.val:
            left = self.traversal(cur.left,p,q)
            if left: return left
        if cur.val< p.val and cur.val<q.val:
            right = self.traversal(cur.right,p,q)
            if right: return right
        return cur        

    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        return self.traversal(root,p,q)
### 或者这个精炼的方法
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):

    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        if not root: return None
        if root.val>p.val and root.val>q.val:
            left = self.lowestCommonAncestor(root.left,p,q)
            if left: return left
        elif root.val<p.val and root.val<q.val:
            right = self.lowestCommonAncestor(root.right,p,q)
            if right: return right
        else:
            return root        
```


### 二叉搜索树中的插入操作
### [题目链接](https://leetcode.cn/problems/insert-into-a-binary-search-tree/)
### 终止判据：有空位也就是 null 就把值填入
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def insertIntoBST(self, root, val):
        """
        :type root: TreeNode
        :type val: int
        :rtype: TreeNode
        """
        if not root or root.val == val:
            return TreeNode(val)
        elif root.val > val:
            if not root.left: root.left = TreeNode(val)
            else: root.left = self.insertIntoBST(root.left,val)
        elif root.val < val:
            if not root.right: root.right = TreeNode(val)
            else: root.right = self.insertIntoBST(root.right,val)
        return root
```



### 450删除二叉搜索树中的节点
### [题目链接](https://leetcode.cn/problems/delete-node-in-a-bst/)
### 思路：分五种情况讨论
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def deleteNode(self, root, key):
        """
        :type root: TreeNode
        :type key: int
        :rtype: TreeNode
        """
        if not root:
            return None
        if root.val == key:
            if root.left is None and root.right is None:
                return None
            elif root.left is not None and root.right is None:
                return root.left
            elif root.left is None and root.right is not None:
                return root.right
            elif root.left is not None and root.right is not None:
                cur = root.right
                while cur.left:
                    cur = cur.left#位置替换，右子树的左替代根
                cur.left = root.left#值的替换，左子树的值替代 cur.left
                return root.right
        
        if root.val > key:
            root.left = self.deleteNode(root.left,key)
        if root.val < key:
            root.right = self.deleteNode(root.right,key)
        return root
        


```