# Interval List Intersections



You are given two lists of closed intervals, `firstList` and `secondList`, where `firstList[i] = [starti, endi]` and `secondList[j] = [startj, endj]`. Each list of intervals is pairwise **disjoint** and in **sorted order**.

Return _the intersection of these two interval lists_.

A **closed interval** `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.

The **intersection** of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of `[1, 3]` and `[2, 4]` is `[2, 3]`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

<pre><code>Input: firstList = [[0,2],[5,10],[13,23],[24,25]], secondList = [[1,5],[8,12],[15,24],[25,26]]
<strong>Output:
</strong> [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
</code></pre>

**Example 2:**

<pre><code>Input: firstList = [[1,3],[5,9]], secondList = []
<strong>Output:
</strong> []
</code></pre>

&#x20;

**Constraints:**

* `0 <= firstList.length, secondList.length <= 1000`
* `firstList.length + secondList.length >= 1`
* `0 <= starti < endi <= 109`
* `endi < starti+1`
* `0 <= startj < endj <= 109`
* `endj < startj+1`

## `Solution`

```java
class Solution {
    public int[][] intervalIntersection(int[][] A, int[][] B) {
        List<int[]> res = new LinkedList<>();
        int i = 0, j = 0;
        while (i < A.length && j < B.length) {
            int a1 = A[i][0], a2 = A[i][1];
            int b1 = B[j][0], b2 = B[j][1];

            if (b2 >= a1 && a2 >= b1) {
                res.add(new int[]{
                        Math.max(a1, b1), Math.min(a2, b2)
                });
            }
            if (b2 < a2) {
                j++;
            } else {
                i++;
            }
        }
        return res.toArray(new int[0][0]);
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=986

```
