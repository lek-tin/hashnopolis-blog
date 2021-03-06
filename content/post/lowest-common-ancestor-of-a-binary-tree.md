---
title: "Lowest Common Ancestor of a Binary Tree"
description: "Some description ..."
authors: ["lek-tin"]
tags: ["leetcode", "binary-tree", "recursion", "dfs", "divide-and-conquer"]
categories: ["algorithm"]
date: 2018-11-01T13:18:53-07:00
draft: false
archive: false
---
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the ![definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (**where we allow a node to be a descendant of itself**).”

Given the following binary tree:  root = [3,5,1,6,2,0,8,null,null,7,4]

        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
### Example 1
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of of nodes 5 and 1 is 3.
```
### Example 2
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

#### Note
- All of the nodes' values will be unique.
- p and q are different and both values will exist in the binary tree.

### Solution
Time complexity: `O(n)`
Space complexity: `O(n)`
```python
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
        # Edge/Condition
        # cannot reach p/q in the end
        if not root:
            return None
        # reaches p or q; If p and q are on the same side, the one that is above the other returns
        if root == p or root == q:
            return root

        # Divide
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)

        # Conquer
        if left and right:
            return root
        if not left:
            return right
        if not right:
            return left
```
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return null;
        if (root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        } else if ( left == null && right == null) {
            return null;
        } else {
            return left != null ? left : right;
        }
    }
}
```
DFS using parent pointer
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        stack = [root]
        parentMap = {root: None}

        while p not in parentMap or q not in parentMap:
            curr = stack.pop()

            if curr.left:
                parentMap[curr.left] = curr
                stack.append(curr.left)

            if curr.right:
                parentMap[curr.right] = curr
                stack.append(curr.right)

        parents = set()

        while p:
            parents.add(p)
            p = parentMap[p]

        while q not in parents:
            q = parentMap[q]

        return q
```