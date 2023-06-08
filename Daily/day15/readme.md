### 二叉树正序倒序输出 leetcode 102,107
### 思路：倒序的时候记得[::-1]
### [题目链接](https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/)
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root: return []
        queue = collections.deque([root])
        result = []
        while queue:
            level = []
            for _ in range(len(queue)):
                cur = queue.popleft()
                level.append(cur.val)
                #print(level)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
            result.append(level)
            print(result)
        return result#正序
        return result[::-1]#倒序
```

### 二叉树的右视图 leetcode 199
### 思路 ： 注意新建一个 size，否则会报错,而且此时输出不是数组，而是 list
### [题目链接](https://leetcode.cn/problems/binary-tree-right-side-view/)
```

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # Definition for a binary tree node.
        if not root: return []
        queue = collections.deque([root])
        
        result = []
        while queue:
            size = len(queue)
            for i in range(size):
                cur = queue.popleft()
                if i == size-1:

                    result.append(cur.val)
                    print(result)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
        return result
 
```

### 二叉树的层平均值
### [题目链接](https://leetcode.cn/problems/average-of-levels-in-binary-tree/)
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
import numpy as np
class Solution(object):
    def averageOfLevels(self, root):
        """
        :type root: TreeNode
        :rtype: List[float]
        """
        if not root:
            return []

        queue = collections.deque([root])
        averages = []
        
        while queue:
            size = len(queue)
            level_sum = []
            
            for i in range(size):
                node = queue.popleft()               
                level_sum.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            level = np.mean(level_sum)
            averages.append(level)
        
        return averages
```


### n叉树的层序遍历 leetcode429
### [题目链接](https://leetcode.cn/problems/n-ary-tree-level-order-traversal/)
### 思路：把 cur.left换成 cur.children,加个 for循环
```
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
import collections
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: Node
        :rtype: List[List[int]]
        """
        if not root:
            return []
        queue = collections.deque([root])
        result = []
        while queue:
            level = []
            size = len(queue)
            for _ in range(size):
                cur = queue.popleft()
                level.append(cur.val)
                for child in cur.children:
                    queue.append(child)
            result.append(level)
        return result
```
### 在每个树行中找最大值 leetcode515
### [题目链接](https://leetcode.cn/problems/find-largest-value-in-each-tree-row/submissions/)
### 思路：和前面求均值的类似，用 numpy
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
import numpy as np
class Solution(object):
    def largestValues(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        queue = collections.deque([root])
        result = []
        while queue:
            max_value = []
            size = len(queue)
            for _ in range(size):
                cur = queue.popleft()
                max_value.append(cur.val)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
            level = np.max(max_value)
            result.append(level)
        return result
```


### 填充每个节点的下一个右侧节点指针 leetcode 116
### [题目链接](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/)
### 思路：引入变量 prev，只有当 prev not empty,指向cur（这道题有点疑问）

```
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""
import collections
class Solution(object):
    def connect(self, root):
        """
        :type root: Node
        :rtype: Node
        """
        if not root:
            return root
        queue = collections.deque([root])
        print(queue)
        result = []
        while queue:
            size = len(queue)
            prev = None
            for i in range(size):
                cur = queue.popleft()
                if prev:
                    prev.next = cur
                prev = cur
                if cur.left:queue.append(cur.left)
                if cur.right:queue.append(cur.right)
        return root
```

### 二叉树最小深度 leetcode111
### [题目链接](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)
### 思路：if not 需要同时成立
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        import collections
        queue = collections.deque([root])
        depth = 0
        while queue:
            depth+=1
            level = []
            size = len(queue)
            for _ in range(size):
                cur = queue.popleft()
                if not cur.left and not cur.right:
                    return depth
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)   
        return depth
```



### 226 翻转二叉树
### [题目链接](https://leetcode.cn/problems/invert-binary-tree/submissions/)
### 思路：注意这里 return None，以及不能单纯的交换，而是指针交换
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root:
            return None
        root.left,root.right = root.right,root.left
        self.invertTree(root.left)
        self.invertTree(root.right)
        return root
```

### 101对称二叉树
### [题目链接](https://leetcode.cn/problems/symmetric-tree/)
### 思路：分四种情况，单独用一个函数做对比
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root: return True
        return self.compare(root.left,root.right)
    def compare(self,left,right):
        if left!=None and right == None:
            return False
        elif left == None and right != None:
            return False   
        elif left == None and right == None:
            return True
        #左右均不为空
        elif left.val != right.val:
            return False
        outside = self.compare(left.left,right.right)
        inside = self.compare(left.right,right.left)
        isSame = outside and inside
        return isSame   

```