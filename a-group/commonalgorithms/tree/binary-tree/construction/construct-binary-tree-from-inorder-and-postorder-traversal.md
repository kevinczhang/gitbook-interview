# Construct Binary Tree from Inorder and Postorder Traversal



Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return _the binary tree_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

<pre><code>Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
<strong>Output:
</strong> [3,9,20,null,null,15,7]
</code></pre>

**Example 2:**

<pre><code>Input: inorder = [-1], postorder = [-1]
<strong>Output:
</strong> [-1]
</code></pre>

&#x20;

**Constraints:**

* `1 <= inorder.length <= 3000`
* `postorder.length == inorder.length`
* `-3000 <= inorder[i], postorder[i] <= 3000`
* `inorder` and `postorder` consist of **unique** values.
* Each value of `postorder` also appears in `inorder`.
* `inorder` is **guaranteed** to be the inorder traversal of the tree.
* `postorder` is **guaranteed** to be the postorder traversal of the tree.

```java
class Solution {
    // 存储 inorder 中值到索引的映射
    HashMap<Integer, Integer> valToIndex = new HashMap<>();

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        for (int i = 0; i < inorder.length; i++) {
            valToIndex.put(inorder[i], i);
        }
        return build(inorder, 0, inorder.length - 1,
                    postorder, 0, postorder.length - 1);
    }

    /*
       定义：
       中序遍历数组为 inorder[inStart..inEnd]，
       后序遍历数组为 postorder[postStart..postEnd]，
       构造这个二叉树并返回该二叉树的根节点
    */
    TreeNode build(int[] inorder, int inStart, int inEnd,
                int[] postorder, int postStart, int postEnd) {

        if (inStart > inEnd) {
            return null;
        }
        // root 节点对应的值就是后序遍历数组的最后一个元素
        int rootVal = postorder[postEnd];
        // rootVal 在中序遍历数组中的索引
        int index = valToIndex.get(rootVal);
        // 左子树的节点个数
        int leftSize = index - inStart;
        TreeNode root = new TreeNode(rootVal);
        // 递归构造左右子树
        root.left = build(inorder, inStart, index - 1,
                         postorder, postStart, postStart + leftSize - 1);
        
        root.right = build(inorder, index + 1, inEnd,
                          postorder, postStart + leftSize, postEnd - 1);
        return root;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=106

```
