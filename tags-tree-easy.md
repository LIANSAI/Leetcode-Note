# Tags Tree - easy

---

104 Maximum Depth of Binary Tree

```
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:                #空集的情况
            return 0

        return 1+max(self.maxDepth(root.left),self.maxDepth(root.right))  #max可以求出深度
```

---

110 Balanced Binary Tree

递归算法先展开到底部再逐步计算

```
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def check(root):
            if root is None:
                return 0
            left = check(root.left)
            right = check(root.right)
            
            if left == -1 or right == -1 or abs(left-right)>1:
                return -1
            
            return 1+max(left,right)
        return check(root)!=-1
```

---



