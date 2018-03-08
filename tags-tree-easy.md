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





