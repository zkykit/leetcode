
### 530二叉搜索树的最小绝对差
### [题目链接](https://leetcode.cn/problems/minimum-absolute-difference-in-bst/submissions/)
### 思路：初始化vec 用来放排序后的中序数组，result 用来放abs 的差。终止判据要注意
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def __init__(self):
        self.vec = []
    def traversal(self,root):
        if not root:
            return 0
        self.traversal(root.left)
        self.vec.append(root.val)
        self.traversal(root.right)
    def getMinimumDifference(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        #self.vec = []
        self.traversal(root)
        if len(self.vec)<2:
            return 0
        result = float('inf')
        for i in range(1, len(self.vec)):
            if result > self.vec[i] - self.vec[i-1]:
                result = self.vec[i] - self.vec[i-1]
        return result

```


### 501 二叉搜索树中的众数
### [题目链接](https://leetcode.cn/problems/find-mode-in-binary-search-tree/submissions/)
### 思路：初始化重要，要想清楚；左中右，中序遍历递归
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def __init__(self):
        self.pre = None
        self.maxCount = 0
        self.Count = 0
        self.result = []
    def traversal(self, cur):
        if not cur:
            return 0
        #左
        self.traversal(cur.left)
        #中
        if self.pre == None: self.Count=1
        elif self.pre.val == cur.val:
            self.Count+=1
        else: self.Count=1
        self.pre = cur
        if self.Count == self.maxCount: 
            self.result.append(cur.val)
        if self.Count > self.maxCount: 
            self.maxCount = self.Count; self.result = [cur.val]; 
        #右
        self.traversal(cur.right)
        return self.result
    def findMode(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        self.traversal(root)
        return self.result

```

### 二叉树的最近公共祖先
### [题目链接](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/submissions/)
### 思路：注意这里的判据可能不太好懂,使用后序遍历来实现回溯
```

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
        if root == q or root == p or not root:
            return root
        left = self.lowestCommonAncestor(root.left,p,q)
        right = self.lowestCommonAncestor(root.right,p,q)

        if left is not None and right is not None:
            return root
        elif left is None and right is not None:
            return right
        elif left is not None and right is None:
            return left
        else:
            return None
```