

### 222 完全二叉树的节点个数
### [题目链接](https://leetcode.cn/problems/count-complete-tree-nodes/submissions/)
### 思路：没什么要总结的
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def countNodes(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        import collections
        queue = collections.deque([root])
        node_num = 0
        while queue:
            size = len(queue)
            print(size)
            node_num+=size
            
            for _ in range(size):
                cur = queue.popleft()
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
        return node_num

```