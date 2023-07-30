# Delete Node in a BST

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return _the **root node reference** (possibly updated) of the BST_.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/04/del\_node\_1.jpg)

<pre><code>Input: root = [5,3,6,2,4,null,7], key = 3
<strong>Output:
</strong> [5,4,6,2,null,null,7]
<strong>Explanation:
</strong> Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
</code></pre>

**Example 2:**

<pre><code>Input: root = [5,3,6,2,4,null,7], key = 0
<strong>Output:
</strong> [5,3,6,2,4,null,7]
<strong>Explanation:
</strong> The tree does not contain a node with value = 0.
</code></pre>

**Example 3:**

<pre><code>Input: root = [], key = 0
<strong>Output:
</strong> []
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[0, 104]`.
* `-105 <= Node.val <= 105`
* Each node has a **unique** value.
* `root` is a valid binary search tree.
* `-105 <= key <= 105`

&#x20;

**Follow up:** Could you solve it with time complexity `O(height of tree)`?

## Solution 1

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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        if (root.val == key) {
            // 这两个 if 把情况 1 和 2 都正确处理了
            if (root.left == null) return root.right;
            if (root.right == null) return root.left;
            // 处理情况 3
            // 获得右子树最小的节点
            TreeNode minNode = getMin(root.right);
            // 删除右子树最小的节点
            root.right = deleteNode(root.right, minNode.val);
            // 用右子树最小的节点替换 root 节点
            minNode.left = root.left;
            minNode.right = root.right;
            root = minNode;
        } else if (root.val > key) {
            root.left = deleteNode(root.left, key);
        } else if (root.val < key) {
            root.right = deleteNode(root.right, key);
        }
        return root;
    }

    TreeNode getMin(TreeNode node) {
        // BST 最左边的就是最小的
        while (node.left != null) node = node.left;
        return node;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=450

```

## Solution 2

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param value: Remove the node with given value.
     * @return: The root of the binary search tree after removal.
     */
    public TreeNode removeNode(TreeNode root, int value) {
        if(root == null) return null;
        if(root.val == value) return replaceNode(root);
        
        TreeNode parent = root;
        TreeNode current = (value < root.val) ? root.left : root.right;
        
        while(current != null){
            if(current.val == value){
                if(current == parent.left){
                    parent.left = replaceNode(current);
                } else {
                    parent.right = replaceNode(current);
                }
                return root;
            } else {
                parent = current;
                current = (value < current.val) ? current.left : current.right;
            }
        }
        return root;
    }
    
    TreeNode replaceNode(TreeNode node){
        if(node.left == null && node.right == null) return null;
        if(node.left != null && node.right == null) return node.left;
        if(node.left == null && node.right != null) return node.right;
        
        TreeNode parent = node, current = node.right;
        while(current.left != null){
            parent = current;
            current = current.left;
        }
        
        if(node.right == current){
            current.left = node.left;
        } else {
            parent.left = current.right;
            current.right = node.right;
            current.left = node.left;
        }
        return current;
    }
}

```
