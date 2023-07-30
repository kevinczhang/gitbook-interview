# Daily Temperatures



Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

&#x20;

**Example 1:**

<pre><code>Input: temperatures = [73,74,75,71,69,72,76,73]
<strong>Output:
</strong> [1,1,4,2,1,1,0,0]
</code></pre>

**Example 2:**

<pre><code>Input: temperatures = [30,40,50,60]
<strong>Output:
</strong> [1,1,1,0]
</code></pre>

**Example 3:**

<pre><code>Input: temperatures = [30,60,90]
<strong>Output:
</strong> [1,1,0]
</code></pre>

&#x20;

**Constraints:**

* `1 <= temperatures.length <= 105`
* `30 <= temperatures[i] <= 100`

## `Solution`

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] res = new int[n];
        // 这⾥放元素索引，⽽不是元素
        Stack<Integer> s = new Stack<>();
        /* 单调栈模板 */
        for (int i = n - 1; i >= 0; i--) {
            while (!s.isEmpty() && temperatures[s.peek()] <= temperatures[i]) {
                s.pop();
            }
            // 得到索引间距
            res[i] = s.isEmpty() ? 0 : (s.peek() - i);
            // 将索引⼊栈，⽽不是元素
            s.push(i);
        }
        return res;
    }
}
```
