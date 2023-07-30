# A + B Problem

Write a function that add two numbers A and B.

#### Clarification

Are a and b both `32-bit` integers?

* Yes.

Can I use bit operation?

* Sure you can.

#### Example

**Example 1:**

```
Input:  a = 1, b = 2
Output: 3	
Explanation: return the result of a + b.
```

**Example 2:**

```
Input:  a = -1, b = 1
Output: 0	
Explanation: return the result of a + b.
```

#### Challenge

Of course you can just return a + b to get accepted. But Can you challenge not do it like that?(You should not use `+` or any arithmetic operators.)

```java
public class Solution {
    /**
     * @param a: An integer
     * @param b: An integer
     * @return: The sum of a and b 
     */
    public int aplusb(int a, int b) {
        while (b != 0) {
            // carry now contains common set bits of x and y  
            int carry = a & b;  
            // Sum of bits of x and y where at least one of the bits is not set  
            a = a ^ b;  
            // Carry is shifted by one so that 
            // adding it to x gives the required sum  
            b = carry << 1; 
        }
        return a;
    }
}
```
