# Combinations

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

```
Given two integers n and k, return all possible combinations of 
k numbers out of 1 ... n.

Example
For example,
If n = 4 and k = 2, a solution is:
[[2,4],[3,4],[2,3],[1,2],[1,3],[1,4]]
```

## Solution

```java
public class Solution {
    /**
     * @param n: Given the range of numbers
     * @param k: Given the numbers of combinations
     * @return: All the combinations of k numbers out of 1..n
     */
    public List<List<Integer>> combine(int n, int k) {
	    List<List<Integer>> res = new ArrayList<List<Integer>>();
	    List<Integer> comb = new ArrayList<Integer>();
	    getCombinations(n, k, 1, res, comb);
	    return res;
    }
    
    void getCombinations(int n, int k, int start, 
			List<List<Integer>> res, List<Integer> comb){
        if(comb.size() == k){
            List<Integer> temp = new ArrayList<Integer>(comb);
            res.add(temp);
            return;
        }
        
        for(int i = start; i < n+1; i++){
            comb.add(i);
            getCombinations(n, k, i+1, res, comb);
            comb.remove(comb.size()-1);
        }
    }
}

```
