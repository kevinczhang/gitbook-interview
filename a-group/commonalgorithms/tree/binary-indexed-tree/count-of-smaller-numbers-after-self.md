# Count of Smaller Numbers After Self



You are given an integer array `nums` and you have to return a new `counts` array. The `counts` array has the property where `counts[i]` is the number of smaller elements to the right of `nums[i]`.

&#x20;

**Example 1:**

```
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

**Example 2:**

```
Input: nums = [-1]
Output: [0]
```

**Example 3:**

```
Input: nums = [-1,-1]
Output: [0,0]
```

&#x20;

**Constraints:**

* `1 <= nums.length <= 105`
* `-104 <= nums[i] <= 104`

## Solution

```java
class Solution {
    private void add(int[] bit, int i, int val) {
        for (; i < bit.length; i += i&(-i)) bit[i] += val;
    }

    private int query(int[] bit, int i) {
        int ans = 0;
        for (; i > 0; i -= i&(-i)) ans += bit[i];
        return ans;
    }

    public List<Integer> countSmaller(int[] nums) {
        int[] tmp = nums.clone();
        Arrays.sort(tmp);
        int[] indexes = new int[nums.length];
        for (int i = 0; i < indexes.length; i++)
            indexes[i] = Arrays.binarySearch(tmp, nums[i]);
        int[] bit = new int[indexes.length];
        int[] ans = new int[indexes.length];
        for (int i = indexes.length - 1; i >= 0; i--) {
            ans[i] = query(bit, indexes[i]);
            add(bit, indexes[i]+1, 1);
        }
        List<Integer> res = new ArrayList();
        for(int n : ans)
            res.add(n);
        return res;
    }

```

