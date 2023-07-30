---
description: Map Interface
---

# Map

## Overview

```java
public interface Map<K,V>
```

1. SortedMap is subInterface of Map Interface. TreeMap implemented SortedMap.
2. &#x20;[HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html), [Hashtable](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html) and  [LinkedHashMap](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html) are most common implementations of Map Interface.
3. &#x20;HashMap is implemented as a hash table, and there is no ordering on keys or values.
4. LinkedHashMap preserves the insertion order.
5. Hashtable is synchronized, in contrast to HashMap. It has overhead for synchronization.
6. Hashtable not allow null keys or values, but HashMap does.

## Commonly used Methods

1. &#x20;[`clear`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#clear--)`()`Removes all of the mappings from this map (optional operation).
2. &#x20;[`containsKey`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#containsKey-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `key)`Returns true if this map contains a mapping for the specified key.
3. &#x20;[`containsValue`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#containsValue-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `value)`Returns true if this map maps one or more keys to the specified value.
4. &#x20;[`entrySet`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#entrySet--)`()`Returns a [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) view of the mappings contained in this map.
5. &#x20;[`get`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#get-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `key)`Returns the value to which the specified key is mapped, or `null` if this map contains no mapping for the key.
6. &#x20;[`getOrDefault`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#getOrDefault-java.lang.Object-V-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `key,` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `defaultValue)`Returns the value to which the specified key is mapped, or `defaultValue` if this map contains no mapping for the key.
7. &#x20;[`isEmpty`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#isEmpty--)`()`Returns true if this map contains no key-value mappings.
8. &#x20;[`keySet`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#keySet--)`()`Returns a [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) view of the keys contained in this map.
9. &#x20;[`put`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#put-K-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `key,` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `value)`Associates the specified value with the specified key in this map (optional operation).
10. &#x20;[`putAll`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#putAll-java.util.Map-)`(`[`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)`<? extends` [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)`,? extends` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)`> m)`Copies all of the mappings from the specified map to this map (optional operation).
11. &#x20;[`putIfAbsent`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#putIfAbsent-K-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `key,` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `value)`If the specified key is not already associated with a value (or is mapped to `null`) associates it with the given value and returns `null`, else returns the current value.
12. &#x20;[`remove`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#remove-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `key)`Removes the mapping for a key from this map if it is present (optional operation).
13. &#x20;[`remove`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#remove-java.lang.Object-java.lang.Object-)`(`[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `key,` [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) `value)`Removes the entry for the specified key only if it is currently mapped to the specified value.
14. &#x20;[`replace`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#replace-K-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `key,` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `value)`Replaces the entry for the specified key only if it is currently mapped to some value.
15. &#x20;[`replace`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#replace-K-V-V-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `key,` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `oldValue,` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) `newValue)`Replaces the entry for the specified key only if currently mapped to the specified value.
16. &#x20;[`size`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#size--)`()`Returns the number of key-value mappings in this map.
17. &#x20;[`values`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html#values--)`()`Returns a [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) view of the values contained in this map.

## SortedMap

### Commonly used methods

1. &#x20;[`firstKey`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html#firstKey--)`()`Returns the first (lowest) key currently in this map.
2. &#x20;[`headMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html#headMap-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) `toKey)`Returns a view of the portion of this map whose keys are strictly less than `toKey`.
3. &#x20;[`lastKey`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html#lastKey--)`()`Returns the last (highest) key currently in this map.
4. &#x20;[`subMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html#subMap-K-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) `fromKey,` [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) `toKey)`Returns a view of the portion of this map whose keys range from `fromKey`, inclusive, to `toKey`, exclusive.
5. &#x20;[`tailMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html#tailMap-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) `fromKey)`Returns a view of the portion of this map whose keys are greater than or equal to `fromKey`.

### TreeMap

#### &#x20;Constructors

1. &#x20;[`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#TreeMap--)`()`Constructs a new, empty tree map, using the natural ordering of its keys.
2. &#x20;[`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#TreeMap-java.util.Comparator-)`(`[`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)`<? super` [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`> comparator)`Constructs a new, empty tree map, ordered according to the given comparator.
3. &#x20;[`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#TreeMap-java.util.Map-)`(`[`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)`<? extends` [`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`,? extends` [`V`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)`> m)`Constructs a new tree map containing the same mappings as the given map, ordered according to the _natural ordering_ of its keys.

#### Commonly used methods

1. &#x20;[`ceilingEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#ceilingEntry-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) `key)`Returns a key-value mapping associated with the least key greater than or equal to the given key, or `null` if there is no such key.
2. &#x20;[`ceilingKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#ceilingKey-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) `key)`Returns the least key greater than or equal to the given key, or `null` if there is no such key.
3. &#x20;[`firstEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#firstEntry--)`()`Returns a key-value mapping associated with the least key in this map, or `null` if the map is empty.
4. &#x20;[`firstKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#firstKey--)`()`Returns the first (lowest) key currently in this map.
5. &#x20;[`floorEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#floorEntry-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) `key)`Returns a key-value mapping associated with the greatest key less than or equal to the given key, or `null` if there is no such key.
6. &#x20;[`floorKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#floorKey-K-)`(`[`K`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) `key)`Returns the greatest key less than or equal to the given key, or `null` if there is no such key.
7. &#x20;[`lastEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#lastEntry--)`()`Returns a key-value mapping associated with the greatest key in this map, or `null` if the map is empty.
8. &#x20;[`lastKey`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#lastKey--)`()`Returns the last (highest) key currently in this map.
9. &#x20;[`pollFirstEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#pollFirstEntry--)`()`Removes and returns a key-value mapping associated with the least key in this map, or `null` if the map is empty.
10. &#x20;[`pollLastEntry`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html#pollLastEntry--)`()`Removes and returns a key-value mapping associated with the greatest key in this map, or `null` if the map is empty.
