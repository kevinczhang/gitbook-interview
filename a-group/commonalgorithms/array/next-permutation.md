# Next Permutation

Given a list of integers, which denote a permutation.&#x20;Find the next permutation in ascending order.

#### &#xD;Example&#xD;

For \[1,3,2,3], the next permutation is \[1,3,3,2]

For \[4,3,2,1], the next permutation is \[1,2,3,4]

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: return nothing (void), do not return anything, 
     * modify nums in-place instead
     */
    public int[] nextPermutation(int[] nums) {
        if(nums.length <= 1) return nums;
        
        int indexdisorder = nums.length-1;
        while(indexdisorder > 0 && nums[indexdisorder] <= nums[indexdisorder-1] ){
        	indexdisorder--;
        }        
        if(indexdisorder == 0){
        	reverse(nums, 0, nums.length-1);
        	return nums;
        }
        indexdisorder--;        
        
        int firstlarger = nums.length-1;
        while(nums[firstlarger] <= nums[indexdisorder])  firstlarger--;
                        	
        swap(nums, indexdisorder, firstlarger);
        reverse(nums, indexdisorder+1, nums.length-1);
        return nums;
    }
    
    void reverse(int[] num, int first, int last) {		
	      while(first < last){
		        swap(num, first, last);
		        first++;
		        last--;
	      }
    }

    void swap(int[] num, int first, int last) {
	      num[first] = num[first]+num[last];
	      num[last] = num[first]-num[last];
	      num[first] = num[first]-num[last];
    }
}
```
