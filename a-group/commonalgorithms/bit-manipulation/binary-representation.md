# Binary Representation

Given a (decimal - e.g. 3.72) number that is passed in as a string, return the binary representation that is passed in as a string. If the fractional part of the number can not be represented accurately in binary with at most 32 characters, return ERROR.

```java
public class Solution {
    /**
     *@param n: Given a decimal number that is passed in as a string
     *@return: A string
     */
    public String binaryRepresentation(String n) {
        int intPart = (n.indexOf('.') == -1) ? 
		        Integer.parseInt(n) : Integer.parseInt(n.substring(0, n.indexOf('.')));
        double decimalPart = (n.indexOf('.') == -1) ? 
				    0 : Double.parseDouble(n.substring(n.indexOf('.')));
        StringBuilder res = new StringBuilder();
        
        // Append the integral part
        if(intPart == 0)
            res.append("0");
        else{
            while(intPart > 0){
                res.insert(0, intPart % 2);
                intPart /= 2;
            }
        }
        if(decimalPart == 0) 
            return res.toString();
        res.append(".");
        int decimalCount = 0;
        // Append the decimal part
        while(decimalPart > 0 && decimalCount < 32){
            if(decimalPart * 2 >= 1){
                res.append("1");
                decimalPart = decimalPart*2.0 - 1.0;
            } else {
                res.append("0");
                decimalPart = decimalPart*2;
            }
            decimalCount++;
        }
        if(decimalPart > 0) return "ERROR";
        return res.toString();
    }
}

```
