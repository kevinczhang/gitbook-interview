---
description: Represents a nongeneric collection of key/value pairs.
---

# IDictionary

The [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) interface is the base interface for nongeneric collections of key/value pairs. For the generic version of this interface, see [System.Collections.Generic.IDictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.idictionary-2?view=netcore-2.2).

Each element is a key/value pair stored in a [DictionaryEntry](https://docs.microsoft.com/en-us/dotnet/api/system.collections.dictionaryentry?view=netcore-2.2) object.

### Properties  <a href="#properties" id="properties"></a>

| [IsFixedSize](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.isfixedsize?view=netcore-2.2#System\_Collections\_IDictionary\_IsFixedSize)        | Gets a value indicating whether the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object has a fixed size.                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [IsReadOnly](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.isreadonly?view=netcore-2.2#System\_Collections\_IDictionary\_IsReadOnly)           | Gets a value indicating whether the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object is read-only.                                                                                                       |
| [Item\[Object\]](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.item?view=netcore-2.2#System\_Collections\_IDictionary\_Item\_System\_Object\_) | Gets or sets the element with the specified key.                                                                                                                                                                                                                          |
| [Keys](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.keys?view=netcore-2.2#System\_Collections\_IDictionary\_Keys)                             | Gets an [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2) object containing the keys of the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object.   |
| [Values](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.values?view=netcore-2.2#System\_Collections\_IDictionary\_Values)                       | Gets an [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2) object containing the values in the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object. |

### Methods  <a href="#methods" id="methods"></a>

| [Add(Object, Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.add?view=netcore-2.2#System\_Collections\_IDictionary\_Add\_System\_Object\_System\_Object\_) | Adds an element with the provided key and value to the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object.                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Clear()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.clear?view=netcore-2.2#System\_Collections\_IDictionary\_Clear)                                           | Removes all elements from the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object.                                                                                                                            |
| [Contains(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.contains?view=netcore-2.2#System\_Collections\_IDictionary\_Contains\_System\_Object\_)          | Determines whether the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object contains an element with the specified key.                                                                                        |
| [GetEnumerator()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.getenumerator?view=netcore-2.2#System\_Collections\_IDictionary\_GetEnumerator)                   | Returns an [IDictionaryEnumerator](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionaryenumerator?view=netcore-2.2) object for the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object. |
| [Remove(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary.remove?view=netcore-2.2#System\_Collections\_IDictionary\_Remove\_System\_Object\_)                | Removes the element with the specified key from the [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) object.                                                                                                      |

## Dictionary\<TKey,TValue> Class

[Dictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netcore-2.2) requires an equality implementation to determine whether keys are equal. You can specify an implementation of the [IEqualityComparer\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.iequalitycomparer-1?view=netcore-2.2) generic interface by using a constructor that accepts a `comparer` parameter; if you do not specify an implementation, the default generic equality comparer [EqualityComparer\<T>.Default](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.equalitycomparer-1.default?view=netcore-2.2) is used. If type `TKey` implements the [System.IEquatable\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.iequatable-1?view=netcore-2.2) generic interface, the default equality comparer uses that implementation.

&#x20;For purposes of enumeration, each item in the dictionary is treated as a [KeyValuePair\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.keyvaluepair-2?view=netcore-2.2) structure representing a value and its key. The order in which the items are returned is undefined.

```csharp
class Program
{
    static void Main()
    {
        // Example Dictionary again.
        Dictionary<string, int> d = new Dictionary<string, int>()
        {
            {"cat", 2},
            {"dog", 1},
            {"llama", 0},
            {"iguana", -1}
        };
        // Loop over pairs with foreach.
        foreach (KeyValuePair<string, int> pair in d)
        {
            Console.WriteLine("{0}, {1}", pair.Key, pair.Value);
        }
    }
}
```

### Methods  <a href="#methods" id="methods"></a>

| [Add(TKey, TValue)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.add?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_Add\_\_0\_\_1\_)                           | Adds the specified key and value to the dictionary.                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Clear()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.clear?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_Clear)                                             | Removes all keys and values from the [Dictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netcore-2.2).              |
| [ContainsKey(TKey)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.containskey?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_ContainsKey\_\_0\_)                | Determines whether the [Dictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netcore-2.2) contains the specified key. |
| [ContainsValue(TValue)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.containsvalue?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_ContainsValue\_\_1\_)        | Determines whether the [Dictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netcore-2.2) contains a specific value.  |
| [GetEnumerator()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.getenumerator?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_GetEnumerator)                     | Returns an enumerator that iterates through the [Dictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netcore-2.2).   |
| [Remove(TKey)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.remove?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_Remove\_\_0\_)                               | Removes the value with the specified key from the [Dictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=netcore-2.2). |
| [Remove(TKey, TValue)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.remove?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_Remove\_\_0\_\_1\_\_)                |                                                                                                                                                                                     |
| [TryAdd(TKey, TValue)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.tryadd?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_TryAdd\_\_0\_\_1\_)                  |                                                                                                                                                                                     |
| [TryGetValue(TKey, TValue)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2.trygetvalue?view=netcore-2.2#System\_Collections\_Generic\_Dictionary\_2\_TryGetValue\_\_0\_\_1\_\_) | Gets the value associated with the specified key.                                                                                                                                   |

```csharp
class Program
{
    static void Main()
    {
        var values = new Dictionary<string, string>();
        values.Add("A", "uppercase letter A");
        values.Add("c", "lowercase letter C");

        // Use inline "out string" with TryGetValue.
        if (values.TryGetValue("c", out string description))
        {
            System.Console.WriteLine(description);
        }
        
        // See whether Dictionary contains this string.
        if (values.ContainsKey("apple"))
        {
            int value = values["apple"];
            Console.WriteLine(value);
        }
    }
}
```

## SortedDictionary\<TKey,TValue> Class

&#x20;Represents a collection of key/value pairs that are sorted on the key.

&#x20;The [SortedDictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.sorteddictionary-2?view=netcore-2.2) generic class is a binary search tree with O(log n) retrieval, where n is the number of elements in the dictionary.  Each key/value pair can be retrieved as a [KeyValuePair\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.keyvaluepair-2?view=netcore-2.2) structure, or as a [DictionaryEntry](https://docs.microsoft.com/en-us/dotnet/api/system.collections.dictionaryentry?view=netcore-2.2) through the nongeneric [IDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.collections.idictionary?view=netcore-2.2) interface.&#x20;

[SortedDictionary\<TKey,TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.sorteddictionary-2?view=netcore-2.2) requires a comparer implementation to perform key comparisons. You can specify an implementation of the [IComparer\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.icomparer-1?view=netcore-2.2) generic interface by using a constructor that accepts a `comparer` parameter; if you do not specify an implementation, the default genericcomparer [Comparer\<T>.Default](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.comparer-1.default?view=netcore-2.2) is used. If type `TKey` implements the [System.IComparable\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable-1?view=netcore-2.2) generic interface, the default comparer uses that implementation.
