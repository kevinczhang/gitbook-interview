# Inorder Successor in BST

Given a binary search tree ([See Definition](http://www.lintcode.com/problem/validate-binary-search-tree/)) and a node in it, find the in-order successor of that node in the BST.

If the given node has no in-order successor in the tree, return `null`.

It's guaranteed _p_ is one node in the given tree. (You can directly compare the memory address to find p)

Example

**Example 1:**

```
Input: {1,#,2}, node with value 1
Output: 2
Explanation:
  1
   \
    2
```

**Example 2:**

```
Input: {2,1,3}, node with value 1
Output: 2
Explanation: 
    2
   / \
  1   3
```

## Solution

```java
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        while (root != null && root.val != p.val) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }

        if (root == null) {
            return null;
        }

        if (root.right == null) {
            return successor;
        }

        root = root.right;
        while (root.left != null) {
            root = root.left;
        }

        return root;
    }
}

// version:高频题班
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (root == null || p == null) {
            return null;
        }

        if (root.val <= p.val) {
            return inorderSuccessor(root.right, p);
        } else {
            TreeNode left = inorderSuccessor(root.left, p);
            return (left != null) ? left : root;
        }
    }
}java
```
