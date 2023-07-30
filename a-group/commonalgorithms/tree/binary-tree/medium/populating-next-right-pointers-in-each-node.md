# Populating Next Right Pointers in Each Node



You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/14/116\_sample.png)

<pre><code>Input: root = [1,2,3,4,5,6,7]
<strong>Output:
</strong> [1,#,2,3,#,4,5,6,7,#]
<strong>Explanation: 
</strong>Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
</code></pre>

**Example 2:**

<pre><code>Input: root = []
<strong>Output:
</strong> []
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[0, 212 - 1]`.
* `-1000 <= Node.val <= 1000`

&#x20;

**Follow-up:**

* You may only use constant extra space.
* The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.

### Iterative Solution

```java
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null) return;
        TreeLinkNode top = root;
        while(top.left != null) {
            TreeLinkNode below = top.left;
            below.next = top.right;
            below = below.next;
            TreeLinkNode cur = top;
            while (cur.next != null) {
                cur = cur.next;
                below.next = cur.left;
                below = below.next;
                below.next = cur.right;
                below = below.next;
            }
            top = top.left;
        }        
    }
}
```

### Recursive solution

```java
class Solution {
    // 主函数
    public Node connect(Node root) {
        if (root == null) return null;
        // 遍历「三叉树」，连接相邻节点
        traverse(root.left, root.right);
        return root;
    }

    // 三叉树遍历框架
    void traverse(Node node1, Node node2) {
        if (node1 == null || node2 == null) {
            return;
        }
        /**** 前序位置 ****/
        // 将传入的两个节点穿起来
        node1.next = node2;
        
        // 连接相同父节点的两个子节点
        traverse(node1.left, node1.right);
        traverse(node2.left, node2.right);
        // 连接跨越父节点的两个子节点
        traverse(node1.right, node2.left);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=116
```
