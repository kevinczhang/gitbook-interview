# Minimum Add to Make Parentheses Valid



A parentheses string is valid if and only if:

* It is the empty string,
* It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
* It can be written as `(A)`, where `A` is a valid string.

You are given a parentheses string `s`. In one move, you can insert a parenthesis at any position of the string.

* For example, if `s = "()))"`, you can insert an opening parenthesis to be `"(`**`(`**`)))"` or a closing parenthesis to be `"())`**`)`**`)"`.

Return _the minimum number of moves required to make_ `s` _valid_.

&#x20;

**Example 1:**

<pre><code>Input: s = "())"
<strong>Output:
</strong> 1
</code></pre>

**Example 2:**

<pre><code>Input: s = "((("
<strong>Output:
</strong> 3
</code></pre>

&#x20;

**Constraints:**

* `1 <= s.length <= 1000`
* `s[i]` is either `'('` or `')'`.

## Solution

```java
class Solution {
    public int minAddToMakeValid(String s) {
        // res 记录插入次数
        int res = 0;
        // need 变量记录右括号的需求量
        int need = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                // 对右括号的需求 + 1
                need++;
            }

            if (s.charAt(i) == ')') {
                // 对右括号的需求 - 1
                need--;

                if (need == -1) {
                    need = 0;
                    // 需插入一个左括号
                    res++;
                }
            }
        }

        return res + need;
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=921

```
