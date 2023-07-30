# String methods

## Most commonly used:

```csharp
string testStr = "test";
int strLen = testStr.Count();
bool strCompare = "".Equals(testStr);
bool strompare2 = "test".Equals(testStr, StringComparison.OrdinalIgnoreCase);
testStr = testStr.Trim();
bool strStartWith = testStr.StartsWith("a");
bool strEndWith = testStr.EndsWith("b");
string lowerCaseStr = testStr.ToLower();
string upperCaseStr = testStr.ToUpper();
string covertToString = 1234.ToString();
char c = testStr[0];

var chars = from str in testStr
            orderby c descending
            where c < 2
            select c;
Char.IsDigit(c);
Char.IsLetter(c);
Char.IsLetterOrDigit(c);
Char.IsLower(c);
Char.IsUpper(c);
Char.IsWhiteSpace(c);
Char.ToLower(c);
Char.ToUpper(c);
// String compare
"a".CompareTo("b");// return -1
"b".CompareTo("a");// return 1
```

## Replace and split methods

1. &#x20;[Split(Char\[\])](https://docs.microsoft.com/en-us/dotnet/api/system.string.split?view=netcore-2.2#System\_String\_Split\_System\_Char\_\_\_):  Splits a string into substrings that are based on the characters in an array.
2. &#x20;[Replace(Char, Char)](https://docs.microsoft.com/en-us/dotnet/api/system.string.replace?view=netcore-2.2#System\_String\_Replace\_System\_Char\_System\_Char\_):  Returns a new string in which all occurrences of a specified Unicode character in this instance are replaced with another specified Unicode character.
3. &#x20;[Replace(String, String)](https://docs.microsoft.com/en-us/dotnet/api/system.string.replace?view=netcore-2.2#System\_String\_Replace\_System\_String\_System\_String\_):  Returns a new string in which all occurrences of a specified string in the current instance are replaced with another specified string.
4. &#x20;[Replace(String, String, StringComparison)](https://docs.microsoft.com/en-us/dotnet/api/system.string.replace?view=netcore-2.2#System\_String\_Replace\_System\_String\_System\_String\_System\_StringComparison\_)
5. &#x20;[Join(String or char, String\[\])](https://docs.microsoft.com/en-us/dotnet/api/system.string.join?view=netcore-2.2#System\_String\_Join\_System\_String\_System\_String\_\_\_):  Concatenates all the elements of a string array, using the specified separator between each element.
6. &#x20;[Join(String, IEnumerable\<String>)](https://docs.microsoft.com/en-us/dotnet/api/system.string.join?view=netcore-2.2#System\_String\_Join\_System\_String\_System\_Collections\_Generic\_IEnumerable\_System\_String\_\_):  Concatenates the members of a constructed [IEnumerable\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1?view=netcore-2.2) collection of type [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netcore-2.2), using the specified separator between each member.

```csharp
string data = "there is a/cat";
string[] words = data.Split(new char[] { ' ', '/' }, StringSplitOptions.RemoveEmptyEntries);
string sentence = "10 cats, 20 dogs, 40 fish and 1 programmer.";
string[] digits = Regex.Split(sentence, @"\D+"); // Get all digit sequence as strings.
string[] operands = Regex.Split(operation, @"\s+"); // Split it on whitespace sequences.
string[] uppercaseWords = Regex.Split(sentence, @"\W"); // Get all words.

string[] arr = { "one", "two", "three" };
string.Join(",", arr)
```

## StringBuilder methods

### Constructors  <a href="#constructors" id="constructors"></a>

| [StringBuilder()](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.-ctor?view=netcore-2.2#System\_Text\_StringBuilder\_\_ctor)                         | Initializes a new instance of the [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netcore-2.2) class.                              |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [StringBuilder(Int32)](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.-ctor?view=netcore-2.2#System\_Text\_StringBuilder\_\_ctor\_System\_Int32\_)   | Initializes a new instance of the [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netcore-2.2) class using the specified capacity. |
| [StringBuilder(String)](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.-ctor?view=netcore-2.2#System\_Text\_StringBuilder\_\_ctor\_System\_String\_) | Initializes a new instance of the [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netcore-2.2) class using the specified string.   |

### Properties <a href="#properties" id="properties"></a>

| [Chars\[Int32\]](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.chars?view=netcore-2.2#System\_Text\_StringBuilder\_Chars\_System\_Int32\_) | Gets or sets the character at the specified character position in this instance.                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [Length](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.length?view=netcore-2.2#System\_Text\_StringBuilder\_Length)                        | Gets or sets the length of the current [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netcore-2.2) object. |

#### Methods

| [Append(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.append?view=netcore-2.2#System\_Text\_StringBuilder\_Append\_System\_Object\_)                       | Appends the string representation of a specified object to this instance.                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Clear()](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.clear?view=netcore-2.2#System\_Text\_StringBuilder\_Clear)                                                  | Removes all characters from the current [StringBuilder](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder?view=netcore-2.2) instance. |
| [Insert(Int32, Object)](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.insert?view=netcore-2.2#System\_Text\_StringBuilder\_Insert\_System\_Int32\_System\_Object\_) | Inserts the string representation of an object into this instance at the specified character position.                                                    |
| [Remove(Int32, Int32)](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.remove?view=netcore-2.2#System\_Text\_StringBuilder\_Remove\_System\_Int32\_System\_Int32\_)   | Removes the specified range of characters from this instance.                                                                                             |
| [Replace(Char, Char)](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.replace?view=netcore-2.2#System\_Text\_StringBuilder\_Replace\_System\_Char\_System\_Char\_)    | Replaces all occurrences of a specified character in this instance with another specified character.                                                      |
| [ToString()](https://docs.microsoft.com/en-us/dotnet/api/system.text.stringbuilder.tostring?view=netcore-2.2#System\_Text\_StringBuilder\_ToString)                                         | Converts the value of this instance to a [String](https://docs.microsoft.com/en-us/dotnet/api/system.string?view=netcore-2.2).                            |

