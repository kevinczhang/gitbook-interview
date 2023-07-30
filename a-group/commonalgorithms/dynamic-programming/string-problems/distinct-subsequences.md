# Distinct Subsequences

Given a string **S** and a string **T**, count the number of distinct subsequences of **S** which equals **T**.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ACE"` is a subsequence of `"ABCDE"` while `"AEC"` is not).

**Example 1:**

```
Input: S = "rabbbit", T = "rabbit"
Output: 3
Explanation:

As shown below, there are 3 ways you can generate "rabbit" from S.
(The caret symbol ^ means the chosen letters)

rabbbit
^^^^ ^^
rabbbit
^^ ^^^^
rabbbit
^^^ ^^^
```

**Example 2:**

```
Input: S = "babgbag", T = "bag"
Output: 5
Explanation:

As shown below, there are 5 ways you can generate "bag" from S.
(The caret symbol ^ means the chosen letters)

babgbag
^^ ^
babgbag
^^    ^
babgbag
^    ^^
babgbag
  ^  ^^
babgbag
    ^^^
```

## Solution

```java
public class Solution {
    /**
     * @param S, T: Two string.
     * @return: Count the number of distinct subsequences
     */
    public int numDistinct(String S, String T) {
        int[][] dp = new int[T.length() + 1][S.length() + 1];
        for (int j = 0; j <= S.length(); j++) {  
            dp[0][j] = 1;  
        }  
        for (int i = 1; i <= T.length(); i++) {  
            for (int j = 1; j <= S.length(); j++) {  
                dp[i][j] = dp[i][j - 1];  
                if (T.charAt(i - 1) == S.charAt(j - 1)) {  
                    dp[i][j] += dp[i - 1][j - 1];  
                }
            }
        }  
        return dp[T.length()][S.length()];
    }
}

```

{% hint style="info" %}
设母串的长度为 j, 子串的长度为 i，我们要求的就是长度为 i 的字串在长度为 j 的母串中出现的次数，设为 t\[i]\[j]，若母串的最后一个字符与子串的最后一个字符不同，则长度为 i 的子串在长度为 j 的母串中出现的次数就是母串的前 j - 1 个字符中子串出现的次数，即 t\[i]\[j] = t\[i]\[j - 1]，若母串的最后一个字符与子串的最后一个字符相同，那么除了前 j - 1 个字符出现字串的次数外，还要加上子串的前 i - 1 个字符在母串的前 j - 1 个字符中出现的次数，即 t\[i]\[j] = t\[i]\[j - 1] + t\[i - 1]\[j - 1]。
{% endhint %}
