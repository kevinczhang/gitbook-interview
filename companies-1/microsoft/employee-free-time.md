# Employee Free Time

## Description

We are given a list `schedule` of employees, which represents the working time for each employee.

Each employee has a list of non-overlapping `Intervals`, and these intervals are in sorted order.

Return the list of finite intervals representing common, positive-length free time for all employees, also in sorted order.

The `Intervals` is an 1d-array. Each two numbers shows an interval. For example, `[1,2,8,10]` represents that the employee works in `[1,2]` and `[8,10]`.

Also, we wouldn't include intervals like \[5, 5] in our answer, as they have zero length.

{% hint style="info" %}
1.schedule and schedule\[i] are lists with lengths in range \[1, 100].\
2.0 <= schedule\[i].start < schedule\[i].end <= 10^8.
{% endhint %}



## Example

**Example 1:**

```
Input：schedule = [[1,2,5,6],[1,3],[4,10]]
Output：[(3,4)]
Explanation:
There are a total of three employees, and all common
free time intervals would be [-inf, 1], [3, 4], [10, inf].
We discard any intervals that contain inf as they aren't finite.
```

**Example 2:**

```
Input：schedule = [[1,3,6,7],[2,4],[2,5,9,12]]
Output：[(5,6),(7,9)]
Explanation：
There are a total of three employees, and all common
free time intervals would be [-inf, 1], [5, 6], [7, 9],[12,inf].
We discard any intervals that contain inf as they aren't finite.
```

## **Solution**

```java
/**
 * Definition of Interval:
 * public class Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 * }
 */

public class Solution {
    /**
     * @param schedule: a list schedule of employees
     * @return: Return a list of finite intervals 
     */
    public List<Interval> employeeFreeTime(int[][] schedule) {
        List<Interval> works = new ArrayList<>();
        for (int[] p : schedule) {
            for (int i = 0; i + 1 < p.length; i += 2) {
                works.add(new Interval(p[i], p[i + 1]));
            }
        }


        Collections.sort(works, (a, b) -> {
            if (a.start == b.start) {
                return a.end - b.end;
            }
            return a.start - b.start;
        });
        List<Interval> ans = new ArrayList<>();
        Interval pre = works.get(0);
        for (int i = 1; i < works.size(); i++) {
            Interval cur = works.get(i);
            if (cur.start > pre.end) {
                ans.add(new Interval(pre.end, cur.start));
                pre = cur;
            } else {
                pre.end = Math.max(pre.end, cur.end);
            }
        }

        return ans;
    }
}
```
