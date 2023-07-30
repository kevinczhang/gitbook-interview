# Delete Digits

Given string A representative a positive integer which has N digits, remove any k digits of the number, the remaining digits are arranged according to the original order to become a new positive integer.

Find the smallest integer after remove k digits.&#x20;N <= 240 and k <= N,

#### &#xD;Example&#xD;

Given an integer A = "178542", k = 4&#x20;return a string "12"

```java
public class Solution {
    /**
     * @param A: A positive integer which has N digits, A is a string.
     * @param k: Remove k digits.
     * @return: A string
     */
    public String DeleteDigits(String A, int k) {
        if(k == 0) return A;
        if(A.length() == 0 || A.length() <= k) return "";
        Deque<Character> stack = new ArrayDeque<Character>();
        int removed = 0;
        for(int i = 0; i < A.length(); i++){
            while(removed < k && !stack.isEmpty() && 
                    stack.peekFirst() > A.charAt(i)){
                stack.removeFirst();
                removed++;
            }
            stack.addFirst(A.charAt(i));
        }
        StringBuilder res = new StringBuilder();
        while(!stack.isEmpty()){
            res.append(stack.removeLast());
        }
        
        // Check leading zeros
        int start = 0;
        while(res.charAt(start) == '0'){
            start++;   
        }        
        return (removed == k) ? res.substring(start) : 
            res.substring(start, A.length()-k);
    }
}

```
