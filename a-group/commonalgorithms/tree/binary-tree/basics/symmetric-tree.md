# Symmetric Tree



Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

<pre><code>Input: root = [1,2,2,3,4,4,3]
<strong>Output:
</strong> true
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

<pre><code>Input: root = [1,2,2,null,3,null,3]
<strong>Output:
</strong> false
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree is in the range `[1, 1000]`.
* `-100 <= Node.val <= 100`



**Recursive**

```java
public boolean isSymmetric(TreeNode root) {
    return root == null || isMirror(root.left, root.right);
}
boolean isMirror(TreeNode node1, TreeNode node2) {
    if (node1 == null && node2 == null) return true;
    if (node1 == null || node2 == null) return false;
    if (node1.val != node2.val) return false;
    return isMirror(node1.left, node2.right) && isMirror(node1.right, node2.left);
}
```

Iterative

```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;
    Queue < TreeNode > q = new LinkedList < TreeNode > ();
    q.offer(root.left);
    q.offer(root.right);
    while (!q.isEmpty()) {
        TreeNode n1 = q.poll();
        TreeNode n2 = q.poll();
        if (n1 == null && n2 == null) continue;
        if (n1 == null && n2 != null) return false;
        if (n1 != null && n2 == null) return false;
        if (n1.val != n2.val) return false;
        q.offer(n1.left);
        q.offer(n2.right);
        q.offer(n1.right);
        q.offer(n2.left);
    }
    return true;
}
```
