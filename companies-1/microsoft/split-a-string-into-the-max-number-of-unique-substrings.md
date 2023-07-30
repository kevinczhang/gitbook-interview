# Split a String Into the Max Number of Unique Substrings

Given a string `s`, return _the maximum number of unique substrings that the given string can be split into_.

You can split string `s` into any list of **non-empty substrings**, where the concatenation of the substrings forms the original string. However, you must split the substrings such that all of them are **unique**.

A **substring** is a contiguous sequence of characters within a string.

&#x20;

**Example 1:**

```
Input: s = "ababccc"
Output: 5
Explanation: One way to split maximally is ['a', 'b', 'ab', 'c', 'cc']. Splitting like ['a', 'b', 'a', 'b', 'c', 'cc'] is not valid as you have 'a' and 'b' multiple times.
```

**Example 2:**

```
Input: s = "aba"
Output: 2
Explanation: One way to split maximally is ['a', 'ba'].
```

**Example 3:**

```
Input: s = "aa"
Output: 1
Explanation: It is impossible to split the string any further.
```

## Solution

```java
class Solution {
    public int maxUniqueSplit(String s) {
        return helper(s,new HashSet<String>());
    }
    public int helper(String s,HashSet<String> uniqueSubStrings){
        if(s.length()==0){
            return uniqueSubStrings.size();
        }
        int rtrnVal=0;
        for(int i=1;i<=s.length();i++){
            String str=s.substring(0,i);
            if(!uniqueSubStrings.contains(str)){
                uniqueSubStrings.add(str);
                
                int res=helper(s.substring(i),uniqueSubStrings);
                rtrnVal=Math.max(rtrnVal,res);
                
                uniqueSubStrings.remove(str);
            }
        }
        return rtrnVal;
    }
}
```
