# Tiny URL

## What is tinyurl?&#x20;

tinyurl is a URL service that users enter a long URL and then the service return a shorter and unique url such as "[http://tiny.me/5ie0V2](http://tiny.me/5ie0V2)". The highlight part can be any string with 6 letters containing \[0-9, a-z, A-Z]. That is, 62^6 \~= 56.8 billions unique strings.

## Single Machine Solution&#x20;

On Single Machine Suppose we have a database which contains three columns: id (auto increment), actual url, and shorten url.

Intuitively, we can design a hash function that maps the actual url to shorten url. But string to string mapping is not easy to compute.

Notice that in the database, each record has a unique id associated with it. What if we convert the id to a shorten url? Basically, we need a Bijective function f(x) = y such that&#x20;

* Each x must be associated with one and only one y;
* Each y must be associated with one and only one x.

In our case, the set of x's are integers while the set of y's are 6-letter-long strings. Actually, each 6-letter-long string can be considered as a number too, a 62-base numeric, if we map each distinct character to a number, e.g. 0-0, ..., 9-9, 10-a, 11-b, ..., 35-z, 36-A, ..., 61-Z.&#x20;

Then, the problem becomes Base Conversion problem which is bijection (if not overflowed :).

```java
public String shorturl(int id, int base, HashMap map) {
    StringBuilder res = new StringBuilder();
    while (id > 0) {
        int digit = id % base;
        res.append(map.get(digit));
        id /= base;
    }
    while (res.length() < 6)  res.append('0');
    return res.reverse().toString();
}
```

For each input long url, the corresponding id is auto generated (in O(1) time). The base conversion algorithm runs in O(k) time where k is the number of digits (i.e. k=6).

## On Multiple Machine&#x20;

Suppose the service gets more and more traffic and thus we need to distributed data onto multiple servers.

We can use Distributed Database. But maintenance for such a db would be much more complicated (replicate data across servers, sync among servers to get a unique id, etc.).

Alternatively, we can use Distributed Key-Value Datastore. Some distributed datastore (e.g. Amazon's Dynamo) uses Consistent Hashing to hash servers and inputs into integers and locate the corresponding server using the hash value of the input. We can apply base conversion algorithm on the hash value of the input.

The basic process can be:&#x20;

#### Insert&#x20;

1. Hash an input long url into a single integer;
2. Locate a server on the ring and store the key--longUrl on the server;
3. Compute the shorten url using base conversion (from 10-base to 62-base) and return it to the user.&#x20;

#### Retrieve&#x20;

1. Convert the shorten url back to the key using base conversion (from 62-base to 10-base);
2. Locate the server containing that key and return the longUrl.
