# Permutation in String



Given two strings `s1` and `s2`, return `true` _if_ `s2` _contains a permutation of_ `s1`_, or_ `false` _otherwise_.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

&#x20;

**Example 1:**

<pre><code>Input: s1 = "ab", s2 = "eidbaooo"
<strong>Output:
</strong> true
<strong>Explanation:
</strong> s2 contains one permutation of s1 ("ba").
</code></pre>

**Example 2:**

<pre><code>Input: s1 = "ab", s2 = "eidboaoo"
<strong>Output:
</strong> false
</code></pre>

&#x20;

**Constraints:**

* `1 <= s1.length, s2.length <= 104`
* `s1` and `s2` consist of lowercase English letters.

## Solution

```java
class Solution {
    public:

    // 判断 s 中是否存在 t 的排列
    bool checkInclusion(string t, string s) {
        unordered_map<char, int> need, window;
        for (char c : t) need[c]++;

        int left = 0, right = 0;
        int valid = 0;
        while (right < s.size()) {
            char c = s[right];
            right++;
            // 进行窗口内数据的一系列更新
            if (need.count(c)) {
                window[c]++;
                if (window[c] == need[c])
                    valid++;
            }

            // 判断左侧窗口是否要收缩
            while (right - left >= t.size()) {
                // 在这里判断是否找到了合法的子串
                if (valid == need.size())
                    return true;
                char d = s[left];
                left++;
                // 进行窗口内数据的一系列更新
                if (need.count(d)) {
                    if (window[d] == need[d])
                        valid--;
                    window[d]--;
                }
            }
        }
        // 未找到符合条件的子串
        return false;
    }
};
// 详细解析参见：
// https://labuladong.github.io/article/?qno=567

```
