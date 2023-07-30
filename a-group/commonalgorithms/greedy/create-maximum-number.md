# Create Maximum Number

Given two arrays of length m and n with digits 0-9 representing two numbers. Create the maximum number of length k <= m + n from digits of the two. The relative order of the digits from the same array must be preserved. Return an array of the k digits. You should try to optimize your time and space complexity.

#### Example 1:&#xD;

nums1 = \[3, 4, 6, 5]; nums2 = \[9, 1, 2, 5, 8, 3]; k = 5.    return \[9, 8, 6, 5, 3]

#### Example 2:&#xD;

nums1 = \[6, 7]; nums2 = \[6, 0, 4]; k = 5. return \[6, 7, 6, 0, 4]

#### Example 3:&#xD;

nums1 = \[3, 9]; nums2 = \[8, 9]; k = 3. return \[9, 8, 9]

```java
public class Solution {
        public int[] maxNumber(int[] nums1, int[] nums2, int k) {
            int[] ans = new int[k];
            for(int i = Math.max(0, k-nums2.length); 
                i <= k && i <= nums1.length; ++i){
                int[] candidate = merge(maxArray(nums1, i), 
                                            maxArray(nums2, k-i), k);
                if(greater(candidate, 0, ans, 0))
                    ans = candidate;
            }
            return ans;
        }

        // Given one array of length n, create the maximum number of length k
        public int[] maxArray(int[] nums,int k){
            int[] ans = new int[k];
            int j = 0;
            for(int i = 0; i < nums.length; ++i){
                while(nums.length-i+j > k && j > 0 && ans[j-1] < nums[i]) j--;
                if(j < k)
                    ans[j++] = nums[i];
            }
            return ans;
        }

        // Given two array of length m and n, 
        // create maximum number of length k = m + n.
        private int[] merge(int[] nums1, int[] nums2, int k){
            int[] ans = new int[k];
            int i = 0, j = 0, r = 0;
            while(r < k)
                ans[r++] = greater(nums1, i, nums2, j) ? nums1[i++] : nums2[j++];
            return ans;
        }
    
	      // Compare nums1 with nums2 from index i and j
        boolean greater(int[] nums1, int i, int[] nums2, int j){
            while(i < nums1.length && j < nums2.length && nums1[i] == nums2[j]){
                i++;
                j++;
            }
            return j == nums2.length || (i < nums1.length && nums1[i] > nums2[j]);
        }
}

```
