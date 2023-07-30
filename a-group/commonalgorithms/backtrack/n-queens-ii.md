# N-Queens II



The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return _the number of distinct solutions to the **n-queens puzzle**_.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

<pre><code>Input: n = 4
<strong>Output:
</strong> 2
<strong>Explanation:
</strong> There are two distinct solutions to the 4-queens puzzle as shown.
</code></pre>

**Example 2:**

<pre><code>Input: n = 1
<strong>Output:
</strong> 1
</code></pre>

&#x20;

**Constraints:**

* `1 <= n <= 9`

## `Solution`

```java
class Solution {
    public int totalNQueens(int n) {
    	if(n <= 0) return 0;
		int[] place = new int[n];
		int[] count = new int[1];
		
		placeQueens(count, place, n, 0);
		return count[0];
    }

	private void placeQueens(int[] count, int[] place, int n, int level){
		if(level == n){
			count[0]++;
			return;
		}
		
		for(int i = 0; i < n; i++){
			if(canplace(level,place,i)){
				place[level] = i;
				placeQueens(count, place, n, level + 1);
			}
		}
	}
	
	private boolean canplace(int i, int[] place, int n){
		for(int j = 0; j < i; j++){
			if(place[j] == n)
				return false;
			if(Math.abs(n-place[j]) == i-j)
				return false;
		}		
		return true;
	}
}
```
