---
description: >-
  Exposes an enumerator, which supports a simple iteration over a non-generic
  collection.
---

# IEnumerable and IEnumerator Interfaces

## IEnumerable Interface

IEnumerable is the base interface of all collection classes as shown below. [IEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable?view=netcore-2.2) is the base interface for all non-generic collections that can be enumerated. For the generic version of this interface see [System.Collections.Generic.IEnumerable\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1?view=netcore-2.2). [IEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable?view=netcore-2.2) contains a single method, [GetEnumerator](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable.getenumerator?view=netcore-2.2), which returns an [IEnumerator](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator?view=netcore-2.2). [IEnumerator](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator?view=netcore-2.2) provides the ability to iterate through the collection by exposing a [Current](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator.current?view=netcore-2.2) property and [MoveNext](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator.movenext?view=netcore-2.2) and [Reset](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator.reset?view=netcore-2.2) methods.

![](<../../../.gitbook/assets/image (6).png>)

&#x20;This interface enables foreach. LINQ acts on IEnumerable things.  We can apply many transformations to an IEnumerable instance, including the ToList and ToArray conversions.

```csharp
IEnumerable<int> result = from value in Enumerable.Range(0, 2)
                                  select value;
foreach (int value in result)
{
   Console.WriteLine(value);
}
```

## IEnumerator Interface

### Properties  <a href="#properties" id="properties"></a>

| [Current](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator.current?view=netframework-4.7.2#System\_Collections\_IEnumerator\_Current) | Gets the element in the collection at the current position of the enumerator. |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |

### Methods  <a href="#methods" id="methods"></a>

| [MoveNext()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator.movenext?view=netframework-4.7.2#System\_Collections\_IEnumerator\_MoveNext) | Advances the enumerator to the next element of the collection.                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| [Reset()](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerator.reset?view=netframework-4.7.2#System\_Collections\_IEnumerator\_Reset)          | Sets the enumerator to its initial position, which is before the first element in the collection. |

## Example of implementing IEnumberable

```csharp
using System;
using System.Collections;

// Simple business object.
public class Person
{
    public Person(string fName, string lName)
    {
        this.firstName = fName;
        this.lastName = lName;
    }

    public string firstName;
    public string lastName;
}

// Collection of Person objects. This class
// implements IEnumerable so that it can be used
// with ForEach syntax.
public class People : IEnumerable
{
    private Person[] _people;
    public People(Person[] pArray)
    {
        _people = new Person[pArray.Length];

        for (int i = 0; i < pArray.Length; i++)
        {
            _people[i] = pArray[i];
        }
    }

// Implementation for the GetEnumerator method.
    IEnumerator IEnumerable.GetEnumerator()
    {
       return (IEnumerator) GetEnumerator();
    }

    public PeopleEnum GetEnumerator()
    {
        return new PeopleEnum(_people);
    }
}

// When you implement IEnumerable, you must also implement IEnumerator.
public class PeopleEnum : IEnumerator
{
    public Person[] _people;

    // Enumerators are positioned before the first element
    // until the first MoveNext() call.
    int position = -1;

    public PeopleEnum(Person[] list)
    {
        _people = list;
    }

    public bool MoveNext()
    {
        position++;
        return (position < _people.Length);
    }

    public void Reset()
    {
        position = -1;
    }

    object IEnumerator.Current
    {
        get
        {
            return Current;
        }
    }

    public Person Current
    {
        get
        {
            try
            {
                return _people[position];
            }
            catch (IndexOutOfRangeException)
            {
                throw new InvalidOperationException();
            }
        }
    }
}

class App
{
    static void Main()
    {
        Person[] peopleArray = new Person[3]
        {
            new Person("John", "Smith"),
            new Person("Jim", "Johnson"),
            new Person("Sue", "Rabon"),
        };

        People peopleList = new People(peopleArray);
        foreach (Person p in peopleList)
            Console.WriteLine(p.firstName + " " + p.lastName);

    }
}
```

## Looping 2D array

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static int[,] _grid = new int[15, 15];
    static void Main()
    {
        _grid[0, 1] = 4;
        _grid[4, 4] = 5;
        _grid[14, 2] = 3;
        int r = 0;
        foreach (int v in GridValues())
        {
            r += v;
        }
        Console.WriteLine(r);
    }
    public static IEnumerable<int> GridValues()
    {
        for (int x = 0; x < 15; x++)
        {
            for (int y = 0; y < 15; y++)
            {
                yield return _grid[x, y];
            }
        }
    }
}
```
