# Unique Binary Search Trees



Given an integer `n`, return _the number of structurally unique **BST'**s (binary search trees) which has exactly_ `n` _nodes of unique values from_ `1` _to_ `n`.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

<pre><code>Input: n = 3
<strong>Output:
</strong> 5
</code></pre>

**Example 2:**

<pre><code>Input: n = 1
<strong>Output:
</strong> 1
</code></pre>

&#x20;

**Constraints:**

* `1 <= n <= 19`

```java
class Solution {
    // 备忘录
    int[][] memo;

    int numTrees(int n) {
        // 备忘录的值初始化为 0
        memo = new int[n + 1][n + 1];
        return count(1, n);
    }

    int count(int lo, int hi) {
        if (lo > hi) return 1;
        // 查备忘录
        if (memo[lo][hi] != 0) {
            return memo[lo][hi];
        }

        int res = 0;
        for (int mid = lo; mid <= hi; mid++) {
            int left = count(lo, mid - 1);
            int right = count(mid + 1, hi);
            res += left * right;
        }
        // 将结果存入备忘录
        memo[lo][hi] = res;

        return res;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=96

```

{% code title="Solution 2" %}
```java
public class Solution {
    public int numTrees(int n) {
        int[] count = new int[n+1];  
        count[0] =1;  
        count[1] =1;  
        for(int i =2; i<=n; i++){  
             for(int j =0; j<i; j++){  
                  count[i] += count[j]*count[i-j-1];   
             }  
        }  
        return count[n];
    }
}
```
{% endcode %}
