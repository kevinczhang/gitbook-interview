# Inorder Successor in BST

Given a binary search tree ([See Definition](http://www.lintcode.com/problem/validate-binary-search-tree/)) and a node in it, find the in-order successor of that node in the BST.

If the given node has no in-order successor in the tree, return `null`.

{% hint style="info" %}
&#x20;It's guaranteed _p_ is one node in the given tree. (You can directly compare the memory address to find p)
{% endhint %}

#### Example

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

#### Challenge

O(h), where h is the height of the BST.

## If tree nodes have pointer to their parents.&#x20;

Can apply to binary tree

```java
public TreeNode withPointerToParent(TreeNode root, TreeNode x) {
		TreeNode successor = null;
		if(x.right != null) {
			successor = x.right;
			while(successor.left != null) {
				successor = successor.left;
			}			
		} else {
			successor = x.parent;
			while (successor != null && x == successor.right) {
				x = successor;
				successor = successor.parent;
			}
		}

		return successor;		
	}
```

## If tree nodes don't have pointer to their parents

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */


public class Solution {
    /*
     * @param root: The root of the BST.
     * @param p: You need find the successor node of p.
     * @return: Successor of p.
     */
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (p == null) return null;
        if (p.right != null) {
            TreeNode cur = p.right;
            while(cur.left != null)
                cur = cur.left;
            return cur;
        } else {
            TreeNode parent = null;
            while (root != null && root.val != p.val) {
                if (root.val > p.val){
                    parent = root;
                    root = root.left;
                } else {
                    root = root.right;
                }
            }
            return (root == null || root.val != p.val) ? null : parent;
        }
    }
}
```
