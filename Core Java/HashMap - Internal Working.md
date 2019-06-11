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

* Initial Empty HashMap
![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/Hashmap_Empty.jpg)

* Inserting Key Value pair
```
map.put("Vishal", 20);
```

**So internally it calls hashCode() method, let's say it returns 118. Then it generates an index by using indexing
algorithm**

So let's say the index comes out to 6. Then it will insert the element in 6th Bucket i.e. 6th array location.
![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/Hashmap_Working_1.jpg)

* Inserting another Key Value Pair
```
map.put("Sachin", 21);
```
So lets say the hashCode comes out to 15 & index comes out to 3.
![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/Hashmap_Working_2.jpg)