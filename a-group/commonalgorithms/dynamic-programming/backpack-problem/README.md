# Backpack Problem

Given n items with size Ai, an integer m denotes the size of a backpack. How full you can fill this backpack?

Example:

If we have 4 items with size \[2, 3, 5, 7], the backpack size is 11, we can select\[2, 3, 5], so that the max size we can fill this backpack is 10. If the backpack size is 12. we can select \[2, 3, 7] so that we can fulfill the backpack.&#x20;

You function should return the max size we can fill in the given backpack.

## Solution

```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        boolean[][] dpTable = new boolean[A.length + 1][m + 1];
        dpTable[0][0] = true;
        
        for(int i = 0; i < A.length; i++){
            for(int j = 0; j <= m; j++){
                dpTable[i+1][j] = (j >= A[i] && dpTable[i][j-A[i]]) ? true : dpTable[i][j];
            }
        }
        for(int i = m; i >=0; i--){
            if(dpTable[A.length][i]) return i;
        }
        return 0;
    }
}

public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        boolean[] dpTable = new boolean[m + 1];
        dpTable[0] = true;
        
        for(int i = 1; i <= A.length; i++){
            for(int j = m; j >= 0; j--){
                dpTable[j] = (j >= A[i-1] && dpTable[j-A[i-1]]) || dpTable[j];
            }
        }
        for(int i = m; i >= 0; i--){
            if(dpTable[i]) return i;
        }
        return 0;
    }
}

```

{% hint style="info" %}
boolean d\[i]\[j]: For the first i items, can we fill a backpack of size j? true or false.&#x20;

d\[i]\[j] = d\[i-1]\[j] || (j>=A\[i-1] && d\[i-1]\[j-A\[i-1]]).&#x20;

d\[0]\[0] = true;&#x20;

We can use 1D array to perform the DP.&#x20;

d\[j] = d\[j] || d\[j-A\[i-1]].&#x20;

NOTE: for 1D array, the j must be decreased from m to 0 rather increasing from 0 to m!
{% endhint %}
