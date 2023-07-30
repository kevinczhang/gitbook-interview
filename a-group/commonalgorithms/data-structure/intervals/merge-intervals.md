# Merge Intervals



Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

&#x20;

**Example 1:**

<pre><code>Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
<strong>Output:
</strong> [[1,6],[8,10],[15,18]]
<strong>Explanation:
</strong> Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
</code></pre>

**Example 2:**

<pre><code>Input: intervals = [[1,4],[4,5]]
<strong>Output:
</strong> [[1,5]]
<strong>Explanation:
</strong> Intervals [1,4] and [4,5] are considered overlapping.
</code></pre>

&#x20;

**Constraints:**

* `1 <= intervals.length <= 104`
* `intervals[i].length == 2`
* `0 <= starti <= endi <= 104`

## `Solution`

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        LinkedList<int[]> res = new LinkedList<>();
        // 按区间的 start 升序排列
        Arrays.sort(intervals, (a, b) -> {
            return a[0] - b[0];
        });

        res.add(intervals[0]);
        for (int i = 1; i < intervals.length; i++) {
            int[] curr = intervals[i];
            // res 中最后一个元素的引用
            int[] last = res.getLast();
            if (curr[0] <= last[1]) {
                last[1] = Math.max(last[1], curr[1]);
            } else {
                // 处理下一个待合并区间
                res.add(curr);
            }
        }
        return res.toArray(new int[0][0]);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=56

```
