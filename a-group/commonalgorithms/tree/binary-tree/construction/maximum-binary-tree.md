# Maximum Binary Tree



You are given an integer array `nums` with no duplicates. A **maximum binary tree** can be built recursively from `nums` using the following algorithm:

1. Create a root node whose value is the maximum value in `nums`.
2. Recursively build the left subtree on the **subarray prefix** to the **left** of the maximum value.
3. Recursively build the right subtree on the **subarray suffix** to the **right** of the maximum value.

Return _the **maximum binary tree** built from_ `nums`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/tree1.jpg)

<pre><code>Input: nums = [3,2,1,6,0,5]
<strong>Output:
</strong> [6,3,5,null,2,0,null,null,1]
<strong>Explanation:
</strong> The recursive calls are as follow:
- The largest value in [3,2,1,6,0,5] is 6. Left prefix is [3,2,1] and right suffix is [0,5].
    - The largest value in [3,2,1] is 3. Left prefix is [] and right suffix is [2,1].
        - Empty array, so no child.
        - The largest value in [2,1] is 2. Left prefix is [] and right suffix is [1].
            - Empty array, so no child.
            - Only one element, so child is a node with value 1.
    - The largest value in [0,5] is 5. Left prefix is [0] and right suffix is [].
        - Only one element, so child is a node with value 0.
        - Empty array, so no child.
</code></pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/24/tree2.jpg)

<pre><code>Input: nums = [3,2,1]
<strong>Output:
</strong> [3,null,2,null,1]
</code></pre>

&#x20;

**Constraints:**

* `1 <= nums.length <= 1000`
* `0 <= nums[i] <= 1000`
* All integers in `nums` are **unique**.

```java
class Solution {
    /* 主函数 */
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return build(nums, 0, nums.length - 1);
    }

    /* 定义：将 nums[lo..hi] 构造成符合条件的树，返回根节点 */
    TreeNode build(int[] nums, int lo, int hi) {
        // base case
        if (lo > hi) {
            return null;
        }

        // 找到数组中的最大值和对应的索引
        int index = -1, maxVal = Integer.MIN_VALUE;
        for (int i = lo; i <= hi; i++) {
            if (maxVal < nums[i]) {
                index = i;
                maxVal = nums[i];
            }
        }

        TreeNode root = new TreeNode(maxVal);
        // 递归调用构造左右子树
        root.left = build(nums, lo, index - 1);
        root.right = build(nums, index + 1, hi);

        return root;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=654

```
