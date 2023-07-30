# Find All Anagrams in a String



Given two strings `s` and `p`, return _an array of all the start indices of_ `p`_'s anagrams in_ `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

&#x20;

**Example 1:**

<pre><code>Input: s = "cbaebabacd", p = "abc"
<strong>Output:
</strong> [0,6]
<strong>Explanation:
</strong>The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
</code></pre>

**Example 2:**

<pre><code>Input: s = "abab", p = "ab"
<strong>Output:
</strong> [0,1,2]
<strong>Explanation:
</strong>The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
</code></pre>

&#x20;

**Constraints:**

* `1 <= s.length, p.length <= 3 * 104`
* `s` and `p` consist of lowercase English letters.

## Solution

```cpp
class Solution {
    public:
    vector<int> findAnagrams(string s, string t) {
        unordered_map<char, int> need, window;
        for (char c : t) need[c]++;

        int left = 0, right = 0;
        int valid = 0;
        vector<int> res; // 记录结果
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
                // 当窗口符合条件时，把起始索引加入 res
                if (valid == need.size())
                    res.push_back(left);
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
        return res;
    }
};
// 详细解析参见：
// https://labuladong.github.io/article/?qno=438

```
