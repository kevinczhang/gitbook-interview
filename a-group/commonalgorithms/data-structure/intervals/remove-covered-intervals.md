# Remove Covered Intervals



Given an array `intervals` where `intervals[i] = [li, ri]` represent the interval `[li, ri)`, remove all intervals that are covered by another interval in the list.

The interval `[a, b)` is covered by the interval `[c, d)` if and only if `c <= a` and `b <= d`.

Return _the number of remaining intervals_.

&#x20;

**Example 1:**

<pre><code>Input: intervals = [[1,4],[3,6],[2,8]]
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> Interval [3,6] is covered by [2,8], therefore it is removed.
</code></pre>

**Example 2:**

<pre><code>Input: intervals = [[1,4],[2,3]]
<strong>Output:
</strong> 1
</code></pre>

&#x20;

**Constraints:**

* `1 <= intervals.length <= 1000`
* `intervals[i].length == 2`
* `0 <= li < ri <= 105`
* All the given intervals are **unique**.

## Solution

```java
class Solution {
    public int removeCoveredIntervals(int[][] intervals) {
        // 按照起点升序排列，起点相同时降序排列
        Arrays.sort(intervals, (a, b) -> {
            if (a[0] == b[0]) {
                return b[1] - a[1];
            }
            return a[0] - b[0];
        });

        // 记录合并区间的起点和终点
        int left = intervals[0][0];
        int right = intervals[0][1];

        int res = 0;
        for (int i = 1; i < intervals.length; i++) {
            int[] intv = intervals[i];
            // 情况一，找到覆盖区间
            if (left <= intv[0] && right >= intv[1]) {
                res++;
            }
            // 情况二，找到相交区间，合并
            if (right >= intv[0] && right <= intv[1]) {
                right = intv[1];
            }
            // 情况三，完全不相交，更新起点和终点
            if (right < intv[0]) {
                left = intv[0];
                right = intv[1];
            }
        }

        return intervals.length - res;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=1288

```
