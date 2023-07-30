# Remove Duplicate Letters

Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

#### Example:&#xD;

Given "bcabc", Return "abc"

Given "cbacdcbc", Return "acdb"

```java
public class Solution {
    public String removeDuplicateLetters(String s) {
        //will contain number of occurences of character (i+'a')
        int[] res = new int[26]; 
        //will contain if character (i+'a') is present in current result Stack
        boolean[] visited = new boolean[26];
        char[] ch = s.toCharArray();
        for(char c : ch){  //count number of occurences of character 
            res[c-'a']++;
        }
        Stack<Character> st = new Stack<>(); // answer stack
        int index;
        for(char c : ch){ 
            index = c - 'a';
             // decrement number of characters remaining 
             // in the string to be analysed
            res[index]--;  
            //if character is already present in stack, dont bother
            if(visited[index]) 
                continue;
            /* if current character is smaller than last character in stack 
            which occurs later in the string again, it can be removed and  
            added later e.g stack = bc remaining string abc then a can pop b 
            and then c */
            while(!st.isEmpty() && c < st.peek() && res[st.peek()-'a'] != 0){ 
                visited[st.pop()-'a']=false;
            }
            //add current character and mark it as visited
            st.push(c); 
            visited[index]=true;
        }

        StringBuilder sb = new StringBuilder();
        //pop character from stack and build answer string from back
        while(!st.isEmpty()){
            sb.insert(0,st.pop());
        }
        return sb.toString();
    }
}

```
