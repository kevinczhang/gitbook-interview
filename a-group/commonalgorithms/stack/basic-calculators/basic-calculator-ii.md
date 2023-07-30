# Basic Calculator II



Given a string `s` which represents an expression, _evaluate this expression and return its value_.&#x20;

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-231, 231 - 1]`.

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

&#x20;

**Example 1:**

<pre><code>Input: s = "3+2*2"
<strong>Output:
</strong> 7
</code></pre>

**Example 2:**

<pre><code>Input: s = " 3/2 "
<strong>Output:
</strong> 1
</code></pre>

**Example 3:**

<pre><code>Input: s = " 3+5 / 2 "
<strong>Output:
</strong> 5
</code></pre>

&#x20;

**Constraints:**

* `1 <= s.length <= 3 * 105`
* `s` consists of integers and operators `('+', '-', '*', '/')` separated by some number of spaces.
* `s` represents **a valid expression**.
* All the integers in the expression are non-negative integers in the range `[0, 231 - 1]`.
* The answer is **guaranteed** to fit in a **32-bit integer**.

## Solution 1

```java
class Solution {
    public int calculate(String s) {

        if (s == null || s.isEmpty()) return 0;
        int len = s.length();
        Stack<Integer> stack = new Stack<Integer>();
        int currentNumber = 0;
        char operation = '+';
        for (int i = 0; i < len; i++) {
            char currentChar = s.charAt(i);
            if (Character.isDigit(currentChar)) {
                currentNumber = (currentNumber * 10) + (currentChar - '0');
            }
            if (!Character.isDigit(currentChar) && !Character.isWhitespace(currentChar) || i == len - 1) {
                if (operation == '-') {
                    stack.push(-currentNumber);
                }
                else if (operation == '+') {
                    stack.push(currentNumber);
                }
                else if (operation == '*') {
                    stack.push(stack.pop() * currentNumber);
                }
                else if (operation == '/') {
                    stack.push(stack.pop() / currentNumber);
                }
                operation = currentChar;
                currentNumber = 0;
            }
        }
        int result = 0;
        while (!stack.isEmpty()) {
            result += stack.pop();
        }
        return result;
    }
}

```

## Solution 2

```java
class Solution {
    public int calculate(String s) {
        int result = 0, curNum = 0, sign = 1;
        int i = 0;
        if (s.charAt(0) == '-'){
            sign = -1;
            i++;
        }
        
        while (i < s.length()) {
            if (Character.isDigit(s.charAt(i))) {
                curNum = curNum * 10 + s.charAt(i) - '0';
            } else if (s.charAt(i) == '+') {
                result += sign*curNum;
                curNum = 0;
                sign = 1;
            } else if (s.charAt(i) == '-') {
                result += sign*curNum;
                curNum = 0;
                sign = -1;
            } else if (s.charAt(i) == '*' || s.charAt(i) == '/') {
                int nextNum = 0;
                char op = s.charAt(i++);
                while (i < s.length() && (s.charAt(i) == ' ' || Character.isDigit(s.charAt(i)))){
                    if (s.charAt(i) == ' '){
                        i++;
                        continue;                        
                    }                    
                    nextNum = nextNum * 10 + s.charAt(i++) - '0';
                }
                curNum = op == '*' ? curNum * nextNum : curNum / nextNum;
                i--;
            }            
            i++;
        }
        result += sign*curNum;
        return result;        
    }
}
```
