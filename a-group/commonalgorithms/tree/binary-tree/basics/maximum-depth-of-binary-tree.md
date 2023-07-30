# Maximum Depth of Binary Tree

Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

<pre><code>Input: root = [3,9,20,null,null,15,7]
<strong>Output:
</strong> 3
</code></pre>

**Example 2:**

<pre><code>Input: root = [1,null,2]
<strong>Output:
</strong> 2
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[0, 104]`.
* `-100 <= Node.val <= 100`

```java
/***** 解法一，回溯算法思路 *****/
class Solution {

    int depth = 0;
    int res = 0;

    public int maxDepth(TreeNode root) {
        traverse(root);
        return res;
    }

    // 遍历二叉树
    void traverse(TreeNode root) {
        if (root == null) {
            return;
        }

        // 前序遍历位置
        depth++;
        // 遍历的过程中记录最大深度
        res = Math.max(res, depth);
        traverse(root.left);
        traverse(root.right);
        // 后序遍历位置
        depth--;
    }
}

/***** 解法二，动态规划思路 *****/
class Solution2 {
    // 定义：输入一个节点，返回以该节点为根的二叉树的最大深度
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftMax = maxDepth(root.left);
        int rightMax = maxDepth(root.right);
        // 根据左右子树的最大深度推出原二叉树的最大深度
        return 1 + Math.max(leftMax, rightMax);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=104

```
