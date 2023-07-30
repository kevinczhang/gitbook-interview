# Minimum Window Substring



Given two strings `s` and `t` of lengths `m` and `n` respectively, return _the **minimum window substring** of_ `s` _such that every character in_ `t` _(**including duplicates**) is included in the window. If there is no such substring, return the empty string_ `""`_._

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

&#x20;

**Example 1:**

<pre><code>Input: s = "ADOBECODEBANC", t = "ABC"
<strong>Output:
</strong> "BANC"
<strong>Explanation:
</strong> The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
</code></pre>

**Example 2:**

<pre><code>Input: s = "a", t = "a"
<strong>Output:
</strong> "a"
<strong>Explanation:
</strong> The entire string s is the minimum window.
</code></pre>

**Example 3:**

<pre><code>Input: s = "a", t = "aa"
<strong>Output:
</strong> ""
<strong>Explanation:
</strong> Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
</code></pre>

&#x20;

**Constraints:**

* `m == s.length`
* `n == t.length`
* `1 <= m, n <= 105`
* `s` and `t` consist of uppercase and lowercase English letters.

## Solution

```java
class Solution {
    public:
    string minWindow(string s, string t) {
        unordered_map<char, int> need, window;
        for (char c : t) need[c]++;

        int left = 0, right = 0;
        int valid = 0;
        // 记录最小覆盖子串的起始索引及长度
        int start = 0, len = INT_MAX;
        while (right < s.size()) {
            // c 是将移入窗口的字符
            char c = s[right];
            // 右移窗口
            right++;
            // 进行窗口内数据的一系列更新
            if (need.count(c)) {
                window[c]++;
                if (window[c] == need[c])
                    valid++;
            }

            // 判断左侧窗口是否要收缩
            while (valid == need.size()) {
                // 在这里更新最小覆盖子串
                if (right - left < len) {
                    start = left;
                    len = right - left;
                }
                // d 是将移出窗口的字符
                char d = s[left];
                // 左移窗口
                left++;
                // 进行窗口内数据的一系列更新
                if (need.count(d)) {
                    if (window[d] == need[d])
                        valid--;
                    window[d]--;
                }
            }
        }
        // 返回最小覆盖子串
        return len == INT_MAX ?
                "" : s.substr(start, len);
    }
};
// 详细解析参见：
// https://labuladong.github.io/article/?qno=76

```
