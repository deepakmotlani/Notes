## HashMap - Internal Working

**HashMap internally maintains array of Node & Node can represent a class with below fields** -
```
K key
V value
int hash
Node next
```

**Hashing is a process of converting an object to integer orm by calling hashCode() method.**

Bucket is 1 element of HashMap array. This Bucket stores elements/nodes. Two or more nodes can have same bucket.
Internally it uses linked structure to connect nodes.

Default array size is 16 i.e. number of Buckets is 16.

