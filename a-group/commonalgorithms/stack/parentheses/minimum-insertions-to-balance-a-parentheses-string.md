# Minimum Insertions to Balance a Parentheses String



Given a parentheses string `s` containing only the characters `'('` and `')'`. A parentheses string is **balanced** if:

* Any left parenthesis `'('` must have a corresponding two consecutive right parenthesis `'))'`.
* Left parenthesis `'('` must go before the corresponding two consecutive right parenthesis `'))'`.

In other words, we treat `'('` as an opening parenthesis and `'))'` as a closing parenthesis.

* For example, `"())"`, `"())(())))"` and `"(())())))"` are balanced, `")()"`, `"()))"` and `"(()))"` are not balanced.

You can insert the characters `'('` and `')'` at any position of the string to balance it if needed.

Return _the minimum number of insertions_ needed to make `s` balanced.

&#x20;

**Example 1:**

<pre><code>Input: s = "(()))"
<strong>Output:
</strong> 1
<strong>Explanation:
</strong> The second '(' has two matching '))', but the first '(' has only ')' matching. We need to add one more ')' at the end of the string to be "(())))" which is balanced.
</code></pre>

**Example 2:**

<pre><code>Input: s = "())"
<strong>Output:
</strong> 0
<strong>Explanation:
</strong> The string is already balanced.
</code></pre>

**Example 3:**

<pre><code>Input: s = "))())("
<strong>Output:
</strong> 3
<strong>Explanation:
</strong> Add '(' to match the first '))', Add '))' to match the last '('.
</code></pre>

&#x20;

**Constraints:**

* `1 <= s.length <= 105`
* `s` consists of `'('` and `')'` only.

## Solution

```java
class Solution {
    public int minInsertions(String s) {
        int res = 0, need = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                need += 2;
                if (need % 2 == 1) {
                    res++;
                    need--;
                }
            }

            if (s.charAt(i) == ')') {
                need--;
                if (need == -1) {
                    res++;
                    need = 1;
                }
            }
        }

        return res + need;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=1541

```
