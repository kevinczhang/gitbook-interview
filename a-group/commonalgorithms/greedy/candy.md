# Candy

There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

* Each child must have at least one candy.
* Children with a higher rating get more candies than their neighbors.

What is the minimum candies you must give?

```java
public class Solution {
    public int candy(int[] ratings) {
        int[] candys = new int[ratings.length];
        //首先每人发一颗糖
        Arrays.fill(candys, 1);
        //这个循环保证了右边高级别的孩子一定比左边的孩子糖果数量多
        for(int i = 1; i < ratings.length; i++) {
            if(ratings[i] > ratings[i - 1]) {
                candys[i] = candys[i - 1] + 1;
            }
        }

        //这个循环保证了左边高级别的孩子一定比右边的孩子糖果数量多
        for(int i = ratings.length - 2; i >= 0; i--) {
            if(ratings[i] > ratings[i + 1] && candys[i] <= candys[i + 1]) {
                candys[i] = candys[i + 1] + 1;
            }
        }

        int n = 0;
        for(int i = 0; i < candys.length; i++) {
            n += candys[i];
        }
        return n;
    }
}

```
