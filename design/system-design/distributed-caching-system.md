# Distributed caching system

Given n cache hosts, an intuitive hash function is key % n. It is simple and commonly used. But it has two major drawbacks:&#x20;

* It is NOT horizontally scalable. Every time when adding one new cache host to the system, all existing mappings are broken. It will be a pain point in maintenance if the caching system contains a lots of data. Also, if the caching system is behind a popular service, it is not easy to schedule a downtime to update all caching mappings.
* It may NOT be load balanced, especially for non-uniformly distributed data. In real world, it is less likely that the data is uniformly distributed. Then for the caching system, it results that some caches are hot and saturated while the others idle and almost empty.&#x20;

In such situations, consistent hashing is a good way to improve the caching system.

## What is Consistent Hashing?&#x20;

Consistent Hashing is a hashing strategy such that when the hash table is resized (e.g. a new cache host is added to the system), only k/n keys need to be remapped, where k is the number of keys and n is the number of caches. Recall that in a caching system using the mod as hash function, all keys need to be remapped.

Consistent hashing maps an object to the same cache host if possible. If a cache host is removed, the objects on that host will be shared by other hosts; If a new cache is added, it takes its share from other hosts without touching other shares.&#x20;

## When to use Consistent Hashing?&#x20;

Consistent hashing is a very useful strategy for distributed caching system and distributed hash tables. It can reduce the impact of host failures. It can also make the caching system more easier to scale up (and scale down).

Example of uses include:&#x20;

* Last.fm: memcached client with consistent hashing
* Amazon: internal scalable key-value store, Dynamo
* Chord: a distributed hash table by MIT&#x20;

## How it works?&#x20;

As a typical hash function, consistent hashing maps a key or a cache host to an integer.

Suppose the output of the hash function are in the range of \[0, 2^128) (e.g. MD5 hash). Image that the integers in the range are placed on a ring such that the values are wrapped around.

Here's how consistent hashing works:

* Given a list of cache servers, hash them to integers in the range.
* To map a key to a server,&#x20;
  * Hash it to a single integer.
  * Move clockwise on the ring until finding the first cache it encounters.&#x20;
  * That cache is the one that contains the key.

To add a new cache, say D, keys that were originally falling to C will be split and some of them will be moved to D. Other keys don't need to be touched.

To remove a cache or if a cache failed, say C, all keys that were originally mapping to C will fall into A and only those keys need to be moved to A. Other keys don't need to be touched.

Now let's consider the load balance issue. As we discussed at the beginning, the real data are essentially randomly distributed and thus may not be uniform. It may cause the keys on caches are unbalanced.

To resolve this issue, we add "virtual replicas" for caches.

* For each cache, instead of mapping it to a single point on the ring, we map it to multiple points on the ring, i.e. replicas.
* By doing this, each cache is associated with multiple segments of the ring.

If the hash function "mixes well", as the number of replicas increases, the keys will be more balanced. See \[3] for a simulation result.&#x20;

#### Monotone Keys&#x20;

If keys are known to be monotonically increased, binary searching can be used to improve the performance of locating a cache for a given key. Then the locate time can be reduced to O(logn).
