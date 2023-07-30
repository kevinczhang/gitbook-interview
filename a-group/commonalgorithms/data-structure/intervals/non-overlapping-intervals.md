# Non-overlapping Intervals



Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return _the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping_.

&#x20;

**Example 1:**

<pre><code>Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
<strong>Output:
</strong> 1
<strong>Explanation:
</strong> [1,3] can be removed and the rest of the intervals are non-overlapping.
</code></pre>

**Example 2:**

<pre><code>Input: intervals = [[1,2],[1,2],[1,2]]
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> You need to remove two [1,2] to make the rest of the intervals non-overlapping.
</code></pre>

**Example 3:**

<pre><code>Input: intervals = [[1,2],[2,3]]
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> You don't need to remove any of the intervals since they're already non-overlapping.
</code></pre>

&#x20;

**Constraints:**

* `1 <= intervals.length <= 105`
* `intervals[i].length == 2`
* `-5 * 104 <= starti < endi <= 5 * 104`

## `Solution`

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        int n = intervals.length;
        return n - intervalSchedule(intervals);
    }

    // 区间调度算法，算出 intvs 中最多有几个互不相交的区间
    int intervalSchedule(int[][] intvs) {
        if (intvs.length == 0) return 0;
        // 按 end 升序排序
        Arrays.sort(intvs, new Comparator<int[]>() {
            public int compare(int[] a, int[] b) {
                return a[1] - b[1];
            }
        });
        // 至少有一个区间不相交
        int count = 1;
        // 排序后，第一个区间就是 x
        int x_end = intvs[0][1];
        for (int[] interval : intvs) {
            int start = interval[0];
            if (start >= x_end) {
                // 找到下一个选择的区间了
                count++;
                x_end = interval[1];
            }
        }
        return count;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=435

```
