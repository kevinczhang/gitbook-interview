# Construct Binary Tree from Preorder and Postorder Traversal



Given two integer arrays, `preorder` and `postorder` where `preorder` is the preorder traversal of a binary tree of **distinct** values and `postorder` is the postorder traversal of the same tree, reconstruct and return _the binary tree_.

If there exist multiple answers, you can **return any** of them.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/24/lc-prepost.jpg)

<pre><code>Input: preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
<strong>Output:
</strong> [1,2,3,4,5,6,7]
</code></pre>

**Example 2:**

<pre><code>Input: preorder = [1], postorder = [1]
<strong>Output:
</strong> [1]
</code></pre>

&#x20;

**Constraints:**

* `1 <= preorder.length <= 30`
* `1 <= preorder[i] <= preorder.length`
* All the values of `preorder` are **unique**.
* `postorder.length == preorder.length`
* `1 <= postorder[i] <= postorder.length`
* All the values of `postorder` are **unique**.
* It is guaranteed that `preorder` and `postorder` are the preorder traversal and postorder traversal of the same binary tree.

```java
class Solution {
    // 存储 postorder 中值到索引的映射
    HashMap<Integer, Integer> valToIndex = new HashMap<>();

    public TreeNode constructFromPrePost(int[] preorder, int[] postorder) {
        for (int i = 0; i < postorder.length; i++) {
            valToIndex.put(postorder[i], i);
        }
        return build(preorder, 0, preorder.length - 1,
                    postorder, 0, postorder.length - 1);
    }

    // 定义：根据 preorder[preStart..preEnd] 和 postorder[postStart..postEnd]
    // 构建二叉树，并返回根节点。
    TreeNode build(int[] preorder, int preStart, int preEnd,
                   int[] postorder, int postStart, int postEnd) {
        if (preStart > preEnd) {
            return null;
        }
        if (preStart == preEnd) {
            return new TreeNode(preorder[preStart]);
        }

        // root 节点对应的值就是前序遍历数组的第一个元素
        int rootVal = preorder[preStart];
        // root.left 的值是前序遍历第二个元素
        // 通过前序和后序遍历构造二叉树的关键在于通过左子树的根节点
        // 确定 preorder 和 postorder 中左右子树的元素区间
        int leftRootVal = preorder[preStart + 1];
        // leftRootVal 在后序遍历数组中的索引
        int index = valToIndex.get(leftRootVal);
        // 左子树的元素个数
        int leftSize = index - postStart + 1;

        // 先构造出当前根节点
        TreeNode root = new TreeNode(rootVal);
        // 递归构造左右子树
        // 根据左子树的根节点索引和元素个数推导左右子树的索引边界
        root.left = build(preorder, preStart + 1, preStart + leftSize,
                postorder, postStart, index);
        root.right = build(preorder, preStart + leftSize + 1, preEnd,
                postorder, index + 1, postEnd - 1);

        return root;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=889

```
