# Delete Operation for Two Strings



Given two strings `word1` and `word2`, return _the minimum number of **steps** required to make_ `word1` _and_ `word2` _the same_.

In one **step**, you can delete exactly one character in either string.

&#x20;

**Example 1:**

<pre><code>Input: word1 = "sea", word2 = "eat"
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
</code></pre>

**Example 2:**

<pre><code>Input: word1 = "leetcode", word2 = "etco"
<strong>Output:
</strong> 4
</code></pre>

&#x20;

**Constraints:**

* `1 <= word1.length, word2.length <= 500`
* `word1` and `word2` consist of only lowercase English letters.

## Solution

```java
class Solution {
    public int minDistance(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        // 复用前文计算 lcs 长度的函数
        int lcs = longestCommonSubsequence(s1, s2);
        return m - lcs + n - lcs;
    }

    // 计算最长公共子序列的长度
    int longestCommonSubsequence(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        // 定义：s1[0..i-1] 和 s2[0..j-1] 的 lcs 长度为 dp[i][j]
        int[][] dp = new int[m + 1][n + 1];

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
// https://labuladong.github.io/article/?qno=583

```
