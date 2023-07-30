# Largest Number

Given a list of non negative integers, arrange them such that they form the largest number.

#### &#xD;Example&#xD;

Given \[1, 20, 23, 4, 8], the largest formed number is 8423201.

```java
public class Solution {
    public String largestNumber(int[] num) {
	String[] numNew = new String[num.length];
        for (int i=0; i<num.length; i++) 
            numNew[i] = String.valueOf(num[i]);        
        Arrays.sort(numNew, NumberComparator);
        StringBuffer strBuf = new StringBuffer();
        for (int i=num.length-1; i>=0; i--) {
            strBuf.append(String.valueOf(numNew[i]));
        }
        return strBuf.charAt(0) == '0' ? "0" : strBuf.toString();
    }
	
    Comparator<String> NumberComparator = new Comparator<String>(){
    	public int compare(String i1, String i2) {       
            int i=0;
            while (i < i1.length() && i < i2.length()) {
                int diff = i1.charAt(i) - i2.charAt(i);
                if (diff == 0) {
                    i++;
                } else {
                    return diff;
                }
            }  
            if (i < i1.length()) {
                return compare(i1.substring(i), i2);
            } else if (i < i2.length()) {
                return compare(i1, i2.substring(i));
            } else {
                return 0;
            }
        }		
    };
}
```

