# Basic Calculator III

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, `+`, `-`, `*`, `/` operators , open `(` and closing parentheses `)` and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-2147483648, 2147483647]`

### Example

**Example 1:**

```
Input："1 + 1"
Output：2
Explanation：1 + 1 = 2
```

**Example 2:**

```
Input：" 6-4 / 2 "
Output：4
Explanation：4/2=2，6-2=4
```

## `Solution 1`

```java
public class Solution {
    /**
     * @param s: the expression string
     * @return: the answer
     */
    public int calculate(String s) {
        if (s == null || s.length() == 0) return 0;
        Stack<Integer> nums = new Stack<>();   //数字栈
        Stack<Character> ops = new Stack<>();   //操作符栈
        int num = 0;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == ' '){
                continue;
            }
            if (Character.isDigit(c)) {			//字符串转化数字
                num = c - '0';
                while (i < s.length() - 1 && Character.isDigit(s.charAt(i + 1))) {
                    num = num * 10 + (s.charAt(i+1) - '0');
                    i++;
                }
                nums.push(num);			//数字直接存入栈中
                num = 0; 
            } else if (c == '(') {		//左括号直接存入
                ops.push(c);
            } else if (c == ')') {		//遇到右括号
                while (ops.peek() != '('){		//对栈顶两数字进行运算
                    nums.push(operation(ops.pop(), nums.pop(), nums.pop()));
                }
                ops.pop(); 
            } else if (c == '+' || c == '-' || c == '*' || c == '/') {   //遇到操作符
                //对栈顶两数字进行运算
                while (!ops.isEmpty() && precedence(c, ops.peek())){                
                    nums.push(operation(ops.pop(), nums.pop(),nums.pop()));
                }
                ops.push(c);
            }
        }
        while (!ops.isEmpty()) {    //取出栈顶的数字进行操作
            nums.push(operation(ops.pop(), nums.pop(), nums.pop()));
        }
        return nums.pop();
    }

    private static int operation(char op, int b, int a) {
        switch (op) {
            case '+': return a + b;   //加法
            case '-': return a - b;	  //减法
            case '*': return a * b;   //乘法
            case '/': return a / b;   //除法
        }
        return 0;
    }
    private static boolean precedence(char op1, char op2) {
        if (op2 == '(' || op2 == ')'){
            return false;
        }
        if ((op1 == '*' || op1 == '/') && (op2 == '+' || op2 == '-')){
            return false;
        }
        return true;
    }
}
```

## Solution 2

```java
public class Solution {
     public int calculate(String s) {
        if(s==null || s.length()==0)
            return 0;
            s=s.trim();
        int res=0, num =0;
        char sign='+';
        Stack<Integer> stack=new Stack();
        for(int i=0;i<s.length();i++){
            char c = s.charAt(i);
            if(Character.isDigit(c)){
                num = num*10+c-'0';
            }
            if(!Character.isDigit(c) || i==s.length()-1){
                if(c==' ') continue;
                if(c=='('){
                    int j=i, cnt=0;
                    while(i<s.length()){
                        if(s.charAt(i)=='(') cnt++;
                        if(s.charAt(i)==')') cnt--;
                        if(cnt==0) break;
                        i++;
                    }
                    num = calculate(s.substring(j+1, i));
                }
                if(sign=='+'){
                    stack.push(num);
                }
                if(sign=='-'){
                    stack.push(-num);
                }
                if(sign=='*'){
                    stack.push(stack.pop()*num);
                }
                if(sign=='/'){
                    stack.push(stack.pop()/num);
                
                }
             num=0;
            sign=c;
            }
        
        }
        while(!stack.isEmpty()){
            res+=stack.pop();
        }
        return res;
    }
}
```
