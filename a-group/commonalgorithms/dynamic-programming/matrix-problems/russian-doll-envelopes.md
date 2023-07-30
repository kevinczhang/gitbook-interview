# Russian Doll Envelopes



You are given a 2D array of integers `envelopes` where `envelopes[i] = [wi, hi]` represents the width and the height of an envelope.

One envelope can fit into another if and only if both the width and height of one envelope are greater than the other envelope's width and height.

Return _the maximum number of envelopes you can Russian doll (i.e., put one inside the other)_.

**Note:** You cannot rotate an envelope.

&#x20;

**Example 1:**

<pre><code>Input: envelopes = [[5,4],[6,4],[6,7],[2,3]]
<strong>Output:
</strong> 3
<strong>Explanation:
</strong> The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
</code></pre>

**Example 2:**

<pre><code>Input: envelopes = [[1,1],[1,1],[1,1]]
<strong>Output:
</strong> 1
</code></pre>

&#x20;

**Constraints:**

* `1 <= envelopes.length <= 105`
* `envelopes[i].length == 2`
* `1 <= wi, hi <= 105`

## `Solution`

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        int n = envelopes.length;
        // 按宽度升序排列，如果宽度一样，则按高度降序排列
        Arrays.sort(envelopes, new Comparator<int[]>() 
        {
            public int compare(int[] a, int[] b) {
                return a[0] == b[0] ? 
                    b[1] - a[1] : a[0] - b[0];
            }
        });
        // 对高度数组寻找 LIS
        int[] height = new int[n];
        for (int i = 0; i < n; i++)
            height[i] = envelopes[i][1];

        return lengthOfLIS(height);
    }

    /* 返回 nums 中 LIS 的长度 */
    public int lengthOfLIS(int[] nums) {
        int piles = 0, n = nums.length;
        int[] top = new int[n];
        for (int i = 0; i < n; i++) {
            // 要处理的扑克牌
            int poker = nums[i];
            int left = 0, right = piles;
            // 二分查找插入位置
            while (left < right) {
                int mid = (left + right) / 2;
                if (top[mid] >= poker)
                    right = mid;
                else
                    left = mid + 1;
            }
            if (left == piles) piles++;
            // 把这张牌放到牌堆顶
            top[left] = poker;
        }
        // 牌堆数就是 LIS 长度
        return piles;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=354

```
