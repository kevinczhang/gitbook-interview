# Advantage Shuffle



You are given two integer arrays `nums1` and `nums2` both of the same length. The **advantage** of `nums1` with respect to `nums2` is the number of indices `i` for which `nums1[i] > nums2[i]`.

Return _any permutation of_ `nums1` _that maximizes its **advantage** with respect to_ `nums2`.

&#x20;

**Example 1:**

<pre><code>Input: nums1 = [2,7,11,15], nums2 = [1,10,4,11]
<strong>Output:
</strong> [2,11,7,15]
</code></pre>

**Example 2:**

<pre><code>Input: nums1 = [12,24,8,32], nums2 = [13,25,32,11]
<strong>Output:
</strong> [24,32,8,12]
</code></pre>

&#x20;

**Constraints:**

* `1 <= nums1.length <= 105`
* `nums2.length == nums1.length`
* `0 <= nums1[i], nums2[i] <= 109`

## `Solution`

```java
class Solution {
    public int[] advantageCount(int[] nums1, int[] nums2) {
        int n = nums1.length;
        // 给 nums2 降序排序
        PriorityQueue<int[]> maxpq = new PriorityQueue<>(
                (int[] pair1, int[] pair2) -> {
                    return pair2[1] - pair1[1];
                }
        );
        for (int i = 0; i < n; i++) {
            maxpq.offer(new int[]{i, nums2[i]});
        }
        // 给 nums1 升序排序
        Arrays.sort(nums1);

        // nums1[left] 是最小值，nums1[right] 是最大值
        int left = 0, right = n - 1;
        int[] res = new int[n];

        while (!maxpq.isEmpty()) {
            int[] pair = maxpq.poll();
            // maxval 是 nums2 中的最大值，i 是对应索引
            int i = pair[0], maxval = pair[1];
            if (maxval < nums1[right]) {
                // 如果 nums1[right] 能胜过 maxval，那就自己上
                res[i] = nums1[right];
                right--;
            } else {
                // 否则用最小值混一下，养精蓄锐
                res[i] = nums1[left];
                left++;
            }
        }
        return res;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=870

```
