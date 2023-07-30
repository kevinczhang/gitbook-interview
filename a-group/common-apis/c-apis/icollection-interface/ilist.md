---
description: >-
  Represents a non-generic collection of objects that can be individually
  accessed by index.
---

# IList

&#x20;[IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) is a descendant of the [ICollection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.icollection?view=netcore-2.2) interface and is the base interface of all non-generic lists. [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2)implementations fall into three categories: read-only, fixed-size, and variable-size. A read-only [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) cannot be modified. A fixed-size [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) does not allow the addition or removal of elements, but it allows the modification of existing elements. A variable-size [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) allows the addition, removal, and modification of elements.

For the generic version of this interface, see [System.Collections.Generic.IList\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ilist-1?view=netcore-2.2).

### Properties  <a href="#properties" id="properties"></a>

| [IsFixedSize](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.isfixedsize?view=netcore-2.2#System\_Collections\_IList\_IsFixedSize)      | Gets a value indicating whether the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) has a fixed size. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| [IsReadOnly](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.isreadonly?view=netcore-2.2#System\_Collections\_IList\_IsReadOnly)         | Gets a value indicating whether the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) is read-only.     |
| [Item\[Int32\]](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.item?view=netcore-2.2#System\_Collections\_IList\_Item\_System\_Int32\_) | Gets or sets the element at the specified index.                                                                                                     |

### Methods  <a href="#methods" id="methods"></a>

| [Add(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.add?view=netcore-2.2#System\_Collections\_IList\_Add\_System\_Object\_)                                | Adds an item to the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2).                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Clear()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.clear?view=netcore-2.2#System\_Collections\_IList\_Clear)                                                  | Removes all items from the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2).                                 |
| [Contains(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.contains?view=netcore-2.2#System\_Collections\_IList\_Contains\_System\_Object\_)                 | Determines whether the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) contains a specific value.           |
| [IndexOf(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.indexof?view=netcore-2.2#System\_Collections\_IList\_IndexOf\_System\_Object\_)                    | Determines the index of a specific item in the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2).             |
| [Insert(Int32, Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.insert?view=netcore-2.2#System\_Collections\_IList\_Insert\_System\_Int32\_System\_Object\_) | Inserts an item to the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) at the specified index.              |
| [Remove(Object)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.remove?view=netcore-2.2#System\_Collections\_IList\_Remove\_System\_Object\_)                       | Removes the first occurrence of a specific object from the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2). |
| [RemoveAt(Int32)](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist.removeat?view=netcore-2.2#System\_Collections\_IList\_RemoveAt\_System\_Int32\_)                   | Removes the [IList](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ilist?view=netcore-2.2) item at the specified index.                    |

```csharp
class Program
{
    static void Main()
    {
        List<int> list = new List<int>(new int[]{ 2, 3, 7 });
        // Loop with for and use string interpolation to print values.
        for (int i = 0; i < list.Count; i++)
        {
            Console.WriteLine($"{i} = {list[i]}");
        }
    }
}
```
