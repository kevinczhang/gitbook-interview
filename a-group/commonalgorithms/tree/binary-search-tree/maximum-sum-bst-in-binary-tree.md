# Maximum Sum BST in Binary Tree



Given a **binary tree** `root`, return _the maximum sum of all keys of **any** sub-tree which is also a Binary Search Tree (BST)_.

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys **less than** the node's key.
* The right subtree of a node contains only nodes with keys **greater than** the node's key.
* Both the left and right subtrees must also be binary search trees.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/01/30/sample\_1\_1709.png)

<pre><code>Input: root = [1,4,3,2,4,2,5,null,null,null,null,null,null,4,6]
<strong>Output:
</strong> 20
<strong>Explanation:
</strong> Maximum sum in a valid Binary search tree is obtained in root node with key equal to 3.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/01/30/sample\_2\_1709.png)

<pre><code>Input: root = [4,3,null,1,2]
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> Maximum sum in a valid Binary search tree is obtained in a single root node with key equal to 2.
</code></pre>

**Example 3:**

<pre><code>Input: root = [-4,-2,-5]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> All values are negatives. Return an empty BST.
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[1, 4 * 104]`.
* `-4 * 104 <= Node.val <= 4 * 104`

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
    // 全局变量，记录 BST 最大节点之和
    int maxSum = 0;

    /* 主函数 */
    public int maxSumBST(TreeNode root) {
        traverse(root);
        return maxSum;
    }

    int[] traverse(TreeNode root) {
        // base case
        if (root == null) {
            return new int[] {
                    1, Integer.MAX_VALUE, Integer.MIN_VALUE, 0
            };
        }

        // 递归计算左右子树
        int[] left = traverse(root.left);
        int[] right = traverse(root.right);

        /*******后序遍历位置*******/
        int[] res = new int[4];
        // 这个 if 在判断以 root 为根的二叉树是不是 BST
        if (left[0] == 1 && right[0] == 1 &&
                root.val > left[2] && root.val < right[1]) {
            // 以 root 为根的二叉树是 BST
            res[0] = 1;
            // 计算以 root 为根的这棵 BST 的最小值
            res[1] = Math.min(left[1], root.val);
            // 计算以 root 为根的这棵 BST 的最大值
            res[2] = Math.max(right[2], root.val);
            // 计算以 root 为根的这棵 BST 所有节点之和
            res[3] = left[3] + right[3] + root.val;
            // 更新全局变量
            maxSum = Math.max(maxSum, res[3]);
        } else {
            // 以 root 为根的二叉树不是 BST
            res[0] = 0;
            // 其他的值都没必要计算了，因为用不到
        }
        /**************************/

        return res;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=1373

```
