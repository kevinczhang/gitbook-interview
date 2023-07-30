# Longest Common Subsequence



Given two strings `text1` and `text2`, return _the length of their longest **common subsequence**._ If there is no **common subsequence**, return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

* For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

&#x20;

**Example 1:**

<pre><code>Input: text1 = "abcde", text2 = "ace" 
<strong>Output:
</strong> 3  
<strong>Explanation:
</strong> The longest common subsequence is "ace" and its length is 3.
</code></pre>

**Example 2:**

<pre><code>Input: text1 = "abc", text2 = "abc"
<strong>Output:
</strong> 3
<strong>Explanation:
</strong> The longest common subsequence is "abc" and its length is 3.
</code></pre>

**Example 3:**

<pre><code>Input: text1 = "abc", text2 = "def"
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> There is no such common subsequence, so the result is 0.
</code></pre>

&#x20;

**Constraints:**

* `1 <= text1.length, text2.length <= 1000`
* `text1` and `text2` consist of only lowercase English characters.

## Solution

```java
class Solution {
    public int longestCommonSubsequence(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        // 定义：s1[0..i-1] 和 s2[0..j-1] 的 lcs 长度为 dp[i][j]
        int[][] dp = new int[m + 1][n + 1];
        // 目标：s1[0..m-1] 和 s2[0..n-1] 的 lcs 长度，即 dp[m][n]
        // base case: dp[0][..] = dp[..][0] = 0

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                // 现在 i 和 j 从 1 开始，所以要减一
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    // s1[i-1] 和 s2[j-1] 必然在 lcs 中
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    // s1[i-1] 和 s2[j-1] 至少有一个不在 lcs 中
                    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
                }
            }
        }

        return dp[m][n];
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=1143

```
