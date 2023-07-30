# Validate Binary Search Tree



Given the `root` of a binary tree, _determine if it is a valid binary search tree (BST)_.

A **valid BST** is defined as follows:

* The left subtree of a node contains only nodes with keys **less than** the node's key.
* The right subtree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right subtrees must also be binary search trees.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

<pre><code>Input: root = [2,1,3]
<strong>Output:
</strong> true
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

<pre><code>Input: root = [5,1,4,null,null,3,6]
<strong>Output:
</strong> false
<strong>Explanation:
</strong> The root node's value is 5 but its right child's value is 4.
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[1, 104]`.
* `-231 <= Node.val <= 231 - 1`

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, null, null);
    }

    /* 限定以 root 为根的子树节点必须满足 max.val > root.val > min.val */
    boolean isValidBST(TreeNode root, TreeNode min, TreeNode max) {
        // base case
        if (root == null) return true;
        // 若 root.val 不符合 max 和 min 的限制，说明不是合法 BST
        if (min != null && root.val <= min.val) return false;
        if (max != null && root.val >= max.val) return false;
        // 限定左子树的最大值是 root.val，右子树的最小值是 root.val
        return isValidBST(root.left, min, root)
                && isValidBST(root.right, root, max);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=98

```
