---
description: Priority Queue
---

# Ugly Number II

Ugly number is a number that only have factors 2, 3 and 5.

Design an algorithm to find the nth ugly number. The first 10 ugly numbers are 1, 2, 3, 4, 5, 6, 8, 9, 10, 12...

{% hint style="info" %}
Note that 1 is typically treated as an ugly number.
{% endhint %}

#### Example&#xD;

If n=9, return 10.

```java
class Solution {
    /**
     * @param n an integer
     * @return the nth prime number as description.
     */
    public int nthUglyNumber(int n) {
        if(n < 7) return n;
        Queue<Long> q = new PriorityQueue<Long>();
        int[] nums = {2,3,5};
        Long result = 1L;
        q.offer(result);
        for(int I = 0; I < n; i++){
            // Each time we poll the peak value of q, is the ith number 
            result = q.poll();
            for(int num : nums){
                Long uglyNum = result*num;
                if(!q.contains(uglyNum)){
                    q.offer(uglyNum);
                }
            }
        }
        return result.intValue();
    }
}

```
