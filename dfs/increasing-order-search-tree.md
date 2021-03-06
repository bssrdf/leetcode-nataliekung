# Increasing Order Search Tree

Given a binary search tree, rearrange the tree in**in-order**so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only 1 right child.

```text
Example 1:
Input:
 [5,3,6,2,4,null,8,1,null,null,null,7,9]

       5
      / \
    3    6
   / \    \
  2   4    8
 /        / \ 
1        7   9


Output:
 [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]

 1
  \
   2
    \
     3
      \
       4
        \
         5
          \
           6
            \
             7
              \
               8
                \
                 9
```

```text
Note:

The number of nodes in the given tree will be between 1 and 100.
Each node will have a unique integer value from 0 to 1000.
```

分析

DFS，这里传入尾做参数，空的时候返回

```text
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def increasingBST(self, root: TreeNode, tail=None) -> TreeNode:       
        if not root:
            return tail

        left = self.increasingBST(root.left,root)        
        root.left = None
        root.right = self.increasingBST(root.right,tail)
        return left
```

