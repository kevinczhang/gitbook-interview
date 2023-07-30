# Find Largest Value in Each Tree Row



Given the `root` of a binary tree, return _an array of the largest value in each row_ of the tree **(0-indexed)**.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/21/largest\_e1.jpg)

<pre><code>Input: root = [1,3,2,5,3,null,9]
<strong>Output:
</strong> [1,3,9]
</code></pre>

**Example 2:**

<pre><code>Input: root = [1,2,3]
<strong>Output:
</strong> [1,3]
</code></pre>

&#x20;

**Constraints:**

* The number of nodes in the tree will be in the range `[0, 104]`.
* `-231 <= Node.val <= 231 - 1`

```java
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        if (root == null) {
            return res;
        }

        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        // while 循环控制从上向下一层层遍历
        while (!q.isEmpty()) {
            int sz = q.size();
            // 记录这一层的最大值
            int levelMax = Integer.MIN_VALUE;
            // for 循环控制每一层从左向右遍历
            for (int i = 0; i < sz; i++) {
                TreeNode cur = q.poll();
                levelMax = Math.max(levelMax, cur.val);
                if (cur.left != null)
                    q.offer(cur.left);
                if (cur.right != null)
                    q.offer(cur.right);
            }
            res.add(levelMax);
        }
        return res;
    }
}

class Solution_DFS {
    // 一定要用 array 存储，因为要用索引随机访问
    ArrayList<Integer> res = new ArrayList<>();

    public List<Integer> largestValues(TreeNode root) {
        if (root == null) {
            return res;
        }
        traverse(root, 0);
        return res;
    }

    // 遍历二叉树
    void traverse(TreeNode root, int depth) {
        if (root == null) {
            return;
        }
        if (res.size() <= depth) {
            res.add(root.val);
        } else {
            // 记录当前行的最大值
            res.set(depth, Math.max(res.get(depth), root.val));
        }
        traverse(root.left, depth + 1);
        traverse(root.right, depth + 1);
    }
}
```
