# First Missing Positive

Given an unsorted integer array, find the first missing positive integer.

```java
public class Solution {
    /**    
     * @param A: an array of integers
     * @return: an integer
     */
    public int firstMissingPositive(int[] A) {
        if(A.length == 0) return 1;
        int i = 0;
        while(i < A.length){
            if(A[i] != i+1 && A[i] >= 1 && A[i] <= A.length && A[A[i]-1] != A[i]){
                int sum = A[i] + A[A[i]-1];
                A[A[i]-1] = sum - A[A[i]-1];
                A[i] = sum - A[i];
            } else {
                i++;
            }
        }
        
        for(int j = 0; j < A.length; j++){
            if(A[j] != j+1) return j + 1;
        }
        return A.length+1;
    }
}

```
