# Text Justification

Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

For example,

words: \["This", "is", "an", "example", "of", "text", "justification."]

L: 16.

Return the formatted lines as:

\[&#x20;  "This    is    an",&#x20;  "example  of text",&#x20;  "justification.  "]

Note: Each word is guaranteed not to exceed L in length.

```java
public class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new ArrayList<String>();
        int i = 0, count = 0, len = 0;
	while(i < words.length){
		len += words[i].length() + 1;			
		if(len - 1 <= maxWidth){
			i++;
			count++;
			continue;
		}
		fillString(words, res, count, i-count, maxWidth);
		len = 0;
		count = 0;
	}
	fillString(words, res, count, i-count, maxWidth);
	return res;
    }

    void fillString(String[] words, List<String> res, 
	int count, int start, int maxWidth){
    
    	StringBuilder sb = new StringBuilder(maxWidth);
	int totalspace = maxWidth;
	for(int i = start; i < start + count; i++) 
		totalspace -= words[i].length();
	// Only one word in this line or last line
	if(count == 1 || start + count == words.length){
		for(int i = start; i < start + count; i++){
			sb.append(words[i]);
			if(totalspace > 0){
				sb.append(" ");
				totalspace--;
			}
		}
		while(totalspace > 0){
			sb.append(" ");
			totalspace--;
		}
		res.add(sb.toString());
		return;
	}
		
	int extraspacelen = totalspace % (count-1);
	StringBuilder evenSpaces = new StringBuilder(totalspace / (count-1));
	for(int i = 0; i < totalspace / (count-1); i++) 
		evenSpaces.append(" ");
	for(int i = start; i < start + count - 1; i++){
		sb.append(words[i]);
		sb.append(evenSpaces);
		if(extraspacelen > 0){
			sb.append(" ");
			extraspacelen--;
		}
	}
        sb.append(words[start + count - 1]);
	res.add(sb.toString());
    }
}

```
