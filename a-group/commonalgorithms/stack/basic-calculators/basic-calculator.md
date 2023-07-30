# Basic Calculator



Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return _the result of the evaluation_.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

&#x20;

**Example 1:**

<pre><code>Input: s = "1 + 1"
<strong>Output:
</strong> 2
</code></pre>

**Example 2:**

<pre><code>Input: s = " 2-1 + 2 "
<strong>Output:
</strong> 3
</code></pre>

**Example 3:**

<pre><code>Input: s = "(1+(4+5+2)-3)+(6+8)"
<strong>Output:
</strong> 23
</code></pre>

&#x20;

**Constraints:**

* `1 <= s.length <= 3 * 105`
* `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.
* `s` represents a valid expression.
* `'+'` is **not** used as a unary operation (i.e., `"+1"` and `"+(2 + 3)"` is invalid).
* `'-'` could be used as a unary operation (i.e., `"-1"` and `"-(2 + 3)"` is valid).
* There will be no two consecutive operators in the input.
* Every number and running calculation will fit in a signed 32-bit integer.

## Solution

```java
class Solution {
    public int calculate(String s) {
        Stack<Integer> stack = new Stack<Integer>();
	    int result = 0, number = 0, sign = 1;
	    for(int i = 0; i < s.length(); i++){
	        char c = s.charAt(i);
	        if(Character.isDigit(c)){
	            number = 10 * number + (int)(c - '0');
	        }else if(c == '+'){
	            result += sign * number;
	            number = 0;
	            sign = 1;
	        }else if(c == '-'){
	            result += sign * number;
	            number = 0;
	            sign = -1;
	        }else if(c == '('){
	            //we push the result first, then sign;
	            stack.push(result);
	            stack.push(sign);
	            //reset the sign and result for the value in the parenthesis
	            sign = 1;   
	            result = 0;
	        }else if(c == ')'){
	            result += sign * number; // result inside the ()	            
	            result *= stack.pop();    //stack.pop() is the sign before the parenthesis
	            result += stack.pop();   //stack.pop() now is the result calculated before the parenthesis
                number = 0;
                sign = 1;
	        }
	    }
	    if(number != 0) result += sign * number;
	    return result;
    }
}
```
