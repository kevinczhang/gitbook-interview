# Remove Duplicate Letters



316\. Remove Duplicate Letters[labuladong 题解](https://labuladong.github.io/article/?qno=316)[思路](https://leetcode.com/problems/remove-duplicate-letters/)Medium5746376Add to ListShare

Given a string `s`, remove duplicate letters so that every letter appears once and only once. You must make sure your result is **the smallest in lexicographical order** among all possible results.

&#x20;

**Example 1:**

<pre><code>Input: s = "bcabc"
<strong>Output:
</strong> "abc"
</code></pre>

**Example 2:**

<pre><code>Input: s = "cbacdcbc"
<strong>Output:
</strong> "acdb"
</code></pre>

&#x20;

**Constraints:**

* `1 <= s.length <= 104`
* `s` consists of lowercase English letters.

## Solution

```java
class Solution {
    public String removeDuplicateLetters(String s) {
        Stack<Character> stk = new Stack<>();

        // 维护一个计数器记录字符串中字符的数量
        // 因为输入为 ASCII 字符，大小 256 够用了
        int[] count = new int[256];
        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i)]++;
        }

        boolean[] inStack = new boolean[256];
        for (char c : s.toCharArray()) {
            // 每遍历过一个字符，都将对应的计数减一
            count[c]--;

            if (inStack[c]) continue;

            while (!stk.isEmpty() && stk.peek() > c) {
                // 若之后不存在栈顶元素了，则停止 pop
                if (count[stk.peek()] == 0) {
                    break;
                }
                // 若之后还有，则可以 pop
                inStack[stk.pop()] = false;
            }
            stk.push(c);
            inStack[c] = true;
        }

        StringBuilder sb = new StringBuilder();
        while (!stk.empty()) {
            sb.append(stk.pop());
        }
        return sb.reverse().toString();
    }
}
// 详细解析参见：
// https://labuladong.github.io/article/?qno=316

```
