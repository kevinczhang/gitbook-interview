---
description: Common algorithms for string
---

# String

## Common methods

Refer to String of Languages section

## KPM for string matching

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

### Solution

For a given source string and a target string, you should output the first index(from 0) of target string in source string. If target does not exist in source, just return -1.

```java
class Solution {
    public int strStr(String haystack, String needle) {
    	if (needle == null || haystack == null || 
    		needle.length() > haystack.length())
            return -1;
        if (needle.length() == 0){
            return 0;
        }
		
	int[] prefixInds = getPrefix(needle);
	int haystackInd = 0;
	while (haystackInd <= haystack.length() - needle.length()) {
		int needleInd = 0;
		while (needleInd < needle.length()) {
		    if(haystack.charAt(haystackInd + needleInd) != needle.charAt(needleInd)) {
			haystackInd = needleInd == 0 ? haystackInd + 1 : 
			haystackInd + needleInd - prefixInds[needleInd - 1];
			break;
		    }
		    needleInd++;
		}
		if (needleInd == needle.length()) {
			return haystackInd;
		}				
	}
	return -1;
    }

    // Generate prefix function for the pattern
    private int[] getPrefix(String pattern) {
	int[] res = new int[pattern.length()];
	res[0] = 0;
	for (int i = 1; i < pattern.length(); i++) {
		int ind = res[i - 1];
		while (ind > 0 && pattern.charAt(ind) != pattern.charAt(i)) {
			ind = res[ind - 1];
		}
		res[i] = (pattern.charAt(ind) == pattern.charAt(i)) ? ind + 1 : 0;
	}		
	return res;
    }
}
```

```java
class Solution1 {
    public int strStr(String haystack, String needle) {

        if (needle == null || haystack == null || 
                needle.length() > haystack.length())
            return -1;
        if (needle.length() == 0){
            return 0;
        }

        int M = needle.length();
        int N = haystack.length();

        // create lps[] that will hold the longest prefix suffix values for pattern
        int j = 0; // index for needle
        // Preprocess the pattern (calculate lps[] array)
        int[] lps = computeLPSArray(needle);

        int i = 0; // index for haystack
        while (i < N) {
            if (needle.charAt(j) == haystack.charAt(i)) {
                j++;
                i++;
            }
            if (j == M) { // Find the match
                return i - M;
            } else if (i < N && needle.charAt(j) != haystack.charAt(i)) { 
                // mismatch after j matches
                // Do not match lps[0..lps[j-1]] characters, they will match anyway
                if (j != 0)
                    j = lps[j - 1];
                else
                    i = i + 1;
            }
        }
        return -1;
    }

    // Generate prefix function for the pattern
    int[] computeLPSArray(String pat) {
        int len = 0; // length of the previous longest prefix suffix
        int i = 1;
        int[] lps = new int[pat.length()];
        lps[0] = 0; // lps[0] is always 0

        while (i < pat.length()) {
            if (pat.charAt(i) == pat.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = len;
                    i++;
                }
            }
        }
        return lps;
    }
}
```

