# Top K Frequent Elements

Given a non-empty array of integers, return the **k** most frequent elements.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**

```
Input: nums = [1], k = 1
Output: [1]
```

**Note:**

* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity **must be** better than O(n log n), where n is the array's size.

## Solution

```java
class Solution {
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> numToCount = new HashMap<>();
        for (int num : nums) {
            if (numToCount.containsKey(num)) {
        	numToCount.put(num, numToCount.get(num) + 1);
            } else {
        	numToCount.put(num, 1);
            }
        }
        
        PriorityQueue<Map.Entry<Integer, Integer>> pq = 
        	new PriorityQueue<>((s1, s2)-> s1.getValue() - s2.getValue());
        
        for(Map.Entry<Integer, Integer> entry : numToCount.entrySet()) {
            if (pq.size() < k) {
        	pq.add(entry);
            } else if (pq.peek().getValue() < entry.getValue()) {
        	pq.poll();
        	pq.add(entry);
            }
        }        
        
        return pq.stream().map(x -> x.getKey()).collect(Collectors.toList());        
    }
}
```
