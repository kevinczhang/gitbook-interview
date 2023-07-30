# Flatten Binary Tree to Linked List

Given the `root` of a binary tree, flatten the tree into a "linked list":

* The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
* The "linked list" should be in the same order as a [**pre-order traversal**](https://en.wikipedia.org/wiki/Tree\_traversal#Pre-order,\_NLR) of the binary tree.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

<pre><code>Input: root = [1,2,5,3,4,null,6]
<strong>Output:
</strong> [1,null,2,null,3,null,4,null,5,null,6]
</code></pre>

**Example 2:**

<pre><code>Input: root = []
<strong>Output:
</strong> []
</code></pre>

**Example 3:**

<pre><code>Input: root = [0]
<strong>Output:
</strong> [0]
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[0, 2000]`.
* `-100 <= Node.val <= 100`

&#x20;

**Follow up:** Can you flatten the tree in-place (with `O(1)` extra space)?

```java
class Solution {
    // 定义：将以 root 为根的树拉平为链表
    public void flatten(TreeNode root) {
        // base case
        if (root == null) return;
        // 先递归拉平左右子树
        flatten(root.left);
        flatten(root.right);

        /****后序遍历位置****/
        // 1、左右子树已经被拉平成一条链表
        TreeNode left = root.left;
        TreeNode right = root.right;

        // 2、将左子树作为右子树
        root.left = null;
        root.right = left;

        // 3、将原先的右子树接到当前右子树的末端
        TreeNode p = root;
        while (p.right != null) {
            p = p.right;
        }
        p.right = right;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=114

```

