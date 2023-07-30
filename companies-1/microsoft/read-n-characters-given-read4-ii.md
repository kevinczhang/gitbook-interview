---
description: '- Call multiple times'
---

# Read N Characters Given Read4 II

## Description

The API: `int read4(char *buf)` reads `4` characters at a time from a file.

The return value is the actual number of characters read. For example, it returns 3 if there is only 3 characters left in the file.

By using the read4 API, implement the function `int read(char *buf, int n)` that reads n characters from the file.

The `read` function may be called multiple times.

Example

**Example 1**

```
Input:
"filetestbuffer"
read(6)
read(5)
read(4)
read(3)
read(2)
read(1)
read(10)
Output:
6, buf = "filete"
5, buf = "stbuf"
3, buf = "fer"
0, buf = ""
0, buf = ""
0, buf = ""
0, buf = ""
```

**Example 2**

```
Input:
"abcdef"
read(1)
read(5)
Output:
1, buf = "a"
5, buf = "bcdef"
```

## Solution

```java
//* The read4 API is defined in the parent class Reader4.
      int read4(char[] buf); */

public class Solution extends Reader4 {
    /**
     * @param buf destination buffer
     * @param n maximum number of characters to read
     * @return the number of characters read
     */
    int readI = 0;
    int writeI = 0;
    char[] buff = new char[4];
    public int read(char[] buf, int n) {
        for (int i = 0; i < n; i++) {
            if (readI == writeI) {
                writeI = read4(buff);
                readI = 0;
                if (writeI == 0) return i;
            }
            buf[i] = buff[readI++];
        }
        return n;
    }
}
```
