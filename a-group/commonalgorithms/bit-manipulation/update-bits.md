# Update Bits

Given two 32-bit numbers, N and M, and two bit positions, iand j. Write a method to set all bits between i and j in N equal to M (e g , M becomes a substring of N located at i and starting at j)

#### &#xD;Clarification&#xD;

You can assume that the bits j through i have enough space to fit all of M. That is, if M=10011， you can assume that there are at least 5 bits between j and i. You would not, for example, have j=3 and i=2, because M could not fully fit between bit 3 and bit 2.

#### Example&#xD;

Given $$N = (10000000000)_2, M = (10101)_2, i = 2, j = 6$$&#x20;

return $$N = (10001010100)_2$$&#x20;

```java
class Solution {
    /**
     *@param n, m: Two integer
     *@param i, j: Two bit positions
     *return: An integer
     */
    public int updateBits(int n, int m, int i, int j) {        
        int left = (j >= 31) ? 0 : ~0 << (j+1);
        int right = ~0 >> (30-i);
        int mask = (left | right);        
        return (n & mask) | (m << i);
    }
}

```
