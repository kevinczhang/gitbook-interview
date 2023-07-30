# Billion pages

You have a billion urls, where each is a huge page. How do you detect the duplicate documents?

## SOLUTION&#x20;

### Observations:&#x20;

1. Pages are huge, so bringing all of them in memory is a costly affair. We need a shorter representation of pages in memory. A hash is an obvious choice for this.
2. Billions of urls exist so we don’t want to compare every page with every other page (that would be O(n^2)).

Based on the above two observations we can derive an algorithm which is as follows:&#x20;

1. Iterate through the pages and compute the hash table of each one.&#x20;
2. Check if the hash value is in the hash table. If it is, throw out the url as a duplicate. If it is not, then keep the url and insert it in into the hash table.&#x20;

This algorithm will provide us a list of unique urls. But wait, can this fit on one computer?&#x20;

*   How much space does each page take up in the hash table?&#x20;

    * Each page hashes to a four byte value.&#x20;
    * Each url is an average of 30 characters, so that’s another 30 bytes at least.&#x20;
    * Each url takes up roughly 34 bytes.&#x20;
    * 34 bytes \* 1 billion = 31.6 gigabytes.&#x20;

    We’re going to have trouble holding that all in memory! What do we do?&#x20;
* We could split this up into files. We’ll have to deal with the file loading / unloading—ugh.&#x20;
* We could hash to disk. Size wouldn’t be a problem, but access time might. A hash table on disk would require a random access read for each check and write to store a viewed url. This could take msecs waiting for seek and rotational latencies. Elevator algorithms could elimate random bouncing from track to track.&#x20;
* Or, we could split this up across machines, and deal with network latency. Let’s go with this solution, and assume we have n machines.&#x20;
  * First, we hash the document to get a hash value v&#x20;
  * v%n tells us which machine this document’s hash table can be found on.&#x20;
  * v / n is the value in the hash table that is located on its machine.
