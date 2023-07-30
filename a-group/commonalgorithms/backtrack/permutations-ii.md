# Permutations II

Given a list of numbers with duplicate number in it. Find allunique permutations.

#### Example&#x20;

For numbers \[1,2,2] the unique permutations are:

```
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
```

## Solution

```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<Integer> cal = new ArrayList<Integer>();
        List<List<Integer>> re = new ArrayList<List<Integer>>();
	Arrays.sort(nums);
	int[] used = new int[nums.length];		
	getpermute(nums, used, cal, re);        
	return re;
    }

    void getpermute(int[] nums, int[] used, List<Integer> cal, List<List<Integer>> re){
	if(cal.size() == nums.length){
		List<Integer> temp = new ArrayList<Integer>(cal);
		re.add(temp);
		return;
	}
	for(int i = 0; i < nums.length; i++){
		if(used[i] == 1) continue;
		cal.add(nums[i]);
		used[i] = 1;
		getpermute(nums, used, cal, re);
		used[i] = 0;
		cal.remove(cal.size()-1);
		while(i < nums.length-1 && nums[i] == nums[i+1]) i++;
	}
    }    
}

```
