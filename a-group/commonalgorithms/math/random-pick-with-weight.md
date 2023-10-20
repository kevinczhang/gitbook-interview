# Random Pick with Weight

You are given a **0-indexed** array of positive integers `w` where `w[i]` describes the **weight** of the `ith` index.

You need to implement the function `pickIndex()`, which **randomly** picks an index in the range `[0, w.length - 1]` (**inclusive**) and returns it. The **probability** of picking an index `i` is `w[i] / sum(w)`.

* For example, if `w = [1, 3]`, the probability of picking index `0` is `1 / (1 + 3) = 0.25` (i.e., `25%`), and the probability of picking index `1` is `3 / (1 + 3) = 0.75` (i.e., `75%`).

&#x20;

**Example 1:**

<pre><code><strong>Input
</strong>["Solution","pickIndex"]
[[[1]],[]]
<strong>Output
</strong>[null,0]

<strong>Explanation
</strong>Solution solution = new Solution([1]);
solution.pickIndex(); // return 0. The only option is to return 0 since there is only one element in w.
</code></pre>

**Example 2:**

<pre><code><strong>Input
</strong>["Solution","pickIndex","pickIndex","pickIndex","pickIndex","pickIndex"]
[[[1,3]],[],[],[],[],[]]
<strong>Output
</strong>[null,1,1,1,1,0]

<strong>Explanation
</strong>Solution solution = new Solution([1, 3]);
solution.pickIndex(); // return 1. It is returning the second element (index = 1) that has a probability of 3/4.
solution.pickIndex(); // return 1
solution.pickIndex(); // return 1
solution.pickIndex(); // return 1
solution.pickIndex(); // return 0. It is returning the first element (index = 0) that has a probability of 1/4.

Since this is a randomization problem, multiple answers are allowed.
All of the following outputs can be considered correct:
[null,1,1,1,1,0]
[null,1,1,1,1,1]
[null,1,1,1,0,0]
[null,1,1,1,0,1]
[null,1,0,1,0,0]
......
and so on.
</code></pre>

&#x20;

**Constraints:**

* `1 <= w.length <= 104`
* `1 <= w[i] <= 105`
* `pickIndex` will be called at most `104` times.



```java
class Solution {
    
    int[] prefixSums;

    public Solution(int[] w) {
        prefixSums = w;
        for (int i = 1; i < w.length; i++) {
            prefixSums[i] += prefixSums[i - 1];
        }
    }
    
    public int pickIndex() {        
        Random rd = new Random();
        int wt = rd.nextInt(prefixSums[prefixSums.length - 1]);        
        int left = 0, right = prefixSums.length, mid;
        while (left < right){
            mid = left + (right - left) /2;
            if (prefixSums[mid] > wt) {
                right = mid;
            } else {
                left = mid + 1;
            }            
        }
        return left;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```
