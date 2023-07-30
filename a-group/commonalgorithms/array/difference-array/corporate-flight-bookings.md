# Corporate Flight Bookings



There are `n` flights that are labeled from `1` to `n`.

You are given an array of flight bookings `bookings`, where `bookings[i] = [firsti, lasti, seatsi]` represents a booking for flights `firsti` through `lasti` (**inclusive**) with `seatsi` seats reserved for **each flight** in the range.

Return _an array_ `answer` _of length_ `n`_, where_ `answer[i]` _is the total number of seats reserved for flight_ `i`.

&#x20;

**Example 1:**

<pre><code>Input: bookings = [[1,2,10],[2,3,20],[2,5,25]], n = 5
<strong>Output:
</strong> [10,55,45,25,25]
<strong>Explanation:
</strong>Flight labels:        1   2   3   4   5
Booking 1 reserved:  10  10
Booking 2 reserved:      20  20
Booking 3 reserved:      25  25  25  25
Total seats:         10  55  45  25  25
Hence, answer = [10,55,45,25,25]
</code></pre>

**Example 2:**

<pre><code>Input: bookings = [[1,2,10],[2,2,15]], n = 2
<strong>Output:
</strong> [10,25]
<strong>Explanation:
</strong>Flight labels:        1   2
Booking 1 reserved:  10  10
Booking 2 reserved:      15
Total seats:         10  25
Hence, answer = [10,25]
</code></pre>

&#x20;

**Constraints:**

* `1 <= n <= 2 * 104`
* `1 <= bookings.length <= 2 * 104`
* `bookings[i].length == 3`
* `1 <= firsti <= lasti <= n`
* `1 <= seatsi <= 104`

## Solution

```java
class Solution {
    public int[] corpFlightBookings(int[][] bookings, int n) {
        int[] nums = new int[n];
        Difference df = new Difference(nums);

        for(int[] booking : bookings){
            int i = booking[0] - 1;
            int j = booking[1] - 1;
            int val = booking[2];
            df.increment(i, j, val);
        }

        return df.result();
    }
}

class Difference{
    private int[] diff;

    public Difference(int[] nums){
        diff = new int[nums.length];
        diff[0] = nums[0];
        for(int i = 1; i < nums.length; i++){
            diff[i] = nums[i]- nums[i-1];
        }
    }

    public void increment(int i, int j, int val){
        diff[i] += val;
        if(j + 1 < diff.length){
            diff[j+1] -= val;
        }
    }

    public int[] result(){
        int[] res = new int[diff.length];
        res[0] = diff[0];
        for(int i = 1; i < diff.length; i++){
            res[i] = res[i-1] + diff[i];
        }
        return res;
    }
}
```
