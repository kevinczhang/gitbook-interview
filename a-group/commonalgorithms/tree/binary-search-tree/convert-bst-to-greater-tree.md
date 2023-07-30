# Convert BST to Greater Tree



Given the `root` of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus the sum of all keys greater than the original key in BST.

As a reminder, a _binary search tree_ is a tree that satisfies these constraints:

* The left subtree of a node contains only nodes with keys **less than** the node's key.
* The right subtree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right subtrees must also be binary search trees.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/05/02/tree.png)

<pre><code>Input: root = [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
<strong>Output:
</strong> [30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
</code></pre>

**Example 2:**

<pre><code>Input: root = [0,null,1]
<strong>Output:
</strong> [1,null,1]
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[0, 104]`.
* `-104 <= Node.val <= 104`
* All the values in the tree are **unique**.
* `root` is guaranteed to be a valid binary search tree.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    TreeNode convertBST(TreeNode root) {
        traverse(root);
        return root;
    }

    // 记录累加和
    int sum = 0;
    void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        traverse(root.right);
        // 维护累加和
        sum += root.val;
        // 将 BST 转化成累加树
        root.val = sum;
        traverse(root.left);
    }

}
```
