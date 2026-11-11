# Array and String

## Arrays methods

1. &#x20;[`asList`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#asList-T...-)`(T... a)`Returns a fixed-size list backed by the specified array.
2. &#x20;[`copyOf`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#copyOf-T:A-int-)`(T[] original, int newLength)`Copies the specified array, truncating or padding with nulls (if necessary) so the copy has the specified length.
3. &#x20;[`copyOfRange`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#copyOfRange-T:A-int-int-)`(T[] original, int from, int to)`Copies the specified range of the specified array into a new array.
4. &#x20;[`equals`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#equals-java.lang.Object:A-java.lang.Object:A-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`[] a,` [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`[] a2)`Returns true if the two specified arrays of Objects are equal to one another.
5. &#x20;[`fill`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#fill-java.lang.Object:A-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`[] a,` [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `val)`Assigns the specified Object reference to each element of the specified array of Objects.
6. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#sort-java.lang.Object:A-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`[] a)`Sorts the specified array of objects into ascending order, according to the [natural ordering](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) of its elements.
7. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#sort-java.lang.Object:A-int-int-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)`[] a, int fromIndex, int toIndex)`Sorts the specified range of the specified array of objects into ascending order, according to the [natural ordering](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) of its elements.
8. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#sort-T:A-java.util.Comparator-)`(T[] a,` [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super T> c)`Sorts the specified array of objects according to the order induced by the specified comparator.
9. &#x20;[`sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#sort-T:A-int-int-java.util.Comparator-)`(T[] a, int fromIndex, int toIndex,` [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super T> c)`Sorts the specified range of the specified array of objects according to the order induced by the specified comparator.

## String methods

```java
String str = "test";
int strLen = testStr.length();
boolean strCompare = "".equals(testStr);
boolean strCompare2 = "abc".equalsIgnoreCase(testStr);
String trimedStr = testStr.trim();
boolean strStartWith = testStr.startsWith("a");
boolean strEndWith = testStr.endsWith("b");
String lowerCaseStr = testStr.toLowerCase();
String upperCaseStr = testStr.toUpperCase();
String covertToString = String.valueOf(1234);
// char in str
char[] strChars = testStr.toCharArray();
char strChar = testStr.charAt(0);
Character.isDigit(strChar);
Character.isLetter(strChar);
Character.isLetterOrDigit(strChar);
Character.isLowerCase(strChar);
Character.isUpperCase(strChar);
Character.isWhitespace(strChar);
Character.toLowerCase(strChar);
Character.toUpperCase(strChar);
```

#### Compares two strings lexicographically:

1. The value 0 if the argument string is equal tothis string;&#x20;
2. A value less than 0 if this string is lexicographically less than the string argument;
3. A value greater than 0 if this string is lexicographically greater than the string argument.

```java
int StrCompareTo = "".compareTo(testStr);
```

### Replace and split methods

1. &#x20;[`replace`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#replace-char-char-)`(char oldChar, char newChar);`Returns a string resulting from replacing all occurrences of `oldChar` in this string with `newChar`.
2. &#x20;[`replaceAll`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#replaceAll-java.lang.String-java.lang.String-)`(`[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `regex,` [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `replacement);`Replaces each substring of this string that matches the given [regular expression](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#sum) with the given replacement.
3. &#x20;[`replaceFirst`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#replaceFirst-java.lang.String-java.lang.String-)`(`[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `regex,` [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `replacement);`Replaces the first substring of this string that matches the given [regular expression](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#sum) with the given replacement.
4. &#x20;[`split`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#split-java.lang.String-)`(`[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `regex);`Splits this string around matches of the given [regular expression](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#sum).
5. &#x20;[`matches`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#matches-java.lang.String-)`(`[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `regex);`Tells whether or not this string matches the given [regular expression](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#sum).

```java
// Split on comma or colon.
String[] parts = testStr.split("[,:]");
// Split on 1+ non-word characters.
String[] words1 = testStr.split("\\W+");
// Separate based on number delimiters.
String[] words2 = testStr.split("\\d+");
// Separate by spaces or , with spaces or . With spaces
String str = "a d, m, i.n";
String delimiters = "\\s+|,\\s*|\\.\\s*";
String[] tokensVal = str.split(delimiters);
// Remove '(' or ')'
String temp = testStr.replaceAll("[()]", "");
// Join strings together
String joinedStr1 = String.join(",", splitedStr);
String joinedStr2 = String.join(",", "test1", "test2");
```

### StringBuilder methods

1. &#x20;[`append`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#append-boolean-)`(obj b);`Appends the string representation of the `object` argument to the sequence.
2. &#x20;[`charAt`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#charAt-int-)`(int index);`Returns the `char` value in this sequence at the specified index.
3. &#x20;[`delete`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#delete-int-int-)`(int start, int end);`Removes the characters in a substring of this sequence
4. &#x20;[`deleteCharAt`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#deleteCharAt-int-)`(int index);`Removes the `char` at the specified position in this sequence.
5. &#x20;[`insert`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#insert-int-java.lang.Object-)`(int offset,` [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `obj);`Inserts the string representation of the `Object` argument into this character sequence.
6. &#x20;[`length`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#length--)`();`Returns the length (character count).
7. &#x20;[`replace`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#replace-int-int-java.lang.String-)`(int start, int end,` [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) `str)`Replaces the characters in a substring of this sequence with characters in the specified `String`.
8. &#x20;[`reverse`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#reverse--)`()`Causes this character sequence to be replaced by the reverse of the sequence.
9. &#x20;[`setCharAt`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#setCharAt-int-char-)`(int index, char ch)`The character at the specified index is set to `ch`.
10. &#x20;[`substring`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#substring-int-)`(int start)`Returns a new `String` that contains a subsequence of characters currently contained in this character sequence.
11. &#x20;[`substring`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#substring-int-int-)`(int start, int end)`Returns a new `String` that contains a subsequence of characters currently contained in this sequence.
12. &#x20;[`toString`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#toString--)`()`Returns a string representing the data in this sequence.
