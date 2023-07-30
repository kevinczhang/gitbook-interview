# Largest Rectangle in Histogram

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](<../../../.gitbook/assets/image (4).png>)

Above is a histogram where width of each bar is 1, given height = \[2,1,5,6,2,3].

![](<../../../.gitbook/assets/image (8).png>)

The largest rectangle is shown in the shaded area, which has area = 10 unit.

For example,&#x20;Given heights = \[2,1,5,6,2,3],&#x20;return 10.

```java
public class Solution {
    public int largestRectangleArea(int[] heights) {
        if (heights == null || heights.length == 0) return 0;
        
        Stack<Integer> stack = new Stack<Integer>();
        int max = 0, i = 0;
 
        while (i < heights.length) {
		//push index to stack when the current height is 
	                // larger than the previous one
	        if (stack.isEmpty() || heights[i] >= heights[stack.peek()]) {
			stack.push(i);
		        i++;
	        } else {
	        //calculate max value when the current height 
	        // is less than the previous one
		       	int p = stack.pop();
		       	max = Math.max(max, 
			heights[p]*(stack.isEmpty() ? i : i - stack.peek() - 1));
	        }
         }
 
         while (!stack.isEmpty()) {
	        int p = stack.pop();
	    	max = Math.max(max, 
			heights[p]*(stack.isEmpty() ? i : i - stack.peek() - 1));
         }
         return max;
    }
}
```

