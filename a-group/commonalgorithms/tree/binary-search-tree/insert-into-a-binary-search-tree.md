# Insert into a Binary Search Tree



You are given the `root` node of a binary search tree (BST) and a `value` to insert into the tree. Return _the root node of the BST after the insertion_. It is **guaranteed** that the new value does not exist in the original BST.

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return **any of them**.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/05/insertbst.jpg)

<pre><code>Input: root = [4,2,7,1,3], val = 5
<strong>Output:
</strong> [4,2,7,1,3,5]
<strong>Explanation:
</strong> Another accepted tree is:
</code></pre>

**Example 2:**

<pre><code>Input: root = [40,20,60,10,30,50,70], val = 25
<strong>Output:
</strong> [40,20,60,10,30,50,70,null,null,25]
</code></pre>

**Example 3:**

<pre><code>Input: root = [4,2,7,1,3,null,null,null,null,null,null], val = 5
<strong>Output:
</strong> [4,2,7,1,3,5]
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree will be in the range `[0, 104]`.
* `-108 <= Node.val <= 108`
* All the values `Node.val` are **unique**.
* `-108 <= val <= 108`
* It's **guaranteed** that `val` does not exist in the original BST.

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        // 找到空位置插入新节点
        if (root == null) return new TreeNode(val);
        // if (root.val == val)
        //     BST 中一般不会插入已存在元素
        if (root.val < val) 
            root.right = insertIntoBST(root.right, val);
        if (root.val > val) 
            root.left = insertIntoBST(root.left, val);
        return root;
    }
}
```
