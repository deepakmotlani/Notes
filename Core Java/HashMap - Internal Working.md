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

* Inserting another Key Value Pair
```
map.put(new Key("vaibhav"), 40);
```
So this again generates hashCode of 11* & index 6. This is a case of **Hash Collision**. In this case it checks
via hashCode() & equals() method to check if both the keys are same. If keys are same it replaces older value with
new one. If it is different then it connects this inserts this node next to last node in linked list.

![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/Hashmap_Working_3.jpg)


## Get elements from HashMap

* When we call the get(key) method, it calls hashCode() method for key to get the hashCode & then calls index() 
method to identify the bucket index. Then it directly goes that bucket.

It picks up the first node & calls equals() method for the keys, if it is equal then it returns this node value.
If it is not equal then it jumps to next node in the linked list. If there is no next node then it returns null.


## HashMap changes in Java 8
Prior to Java 8, we used to do a linear search for elements in linked list. So in worst case the complexity is O(n).

To address this issue, Java 8 uses balanced tree when certain threshold is reached. This means HashMap will start
storing elements in Linked List initially & if certain threshold is reached, it will change to balanced tree.
So it improves complexity from O(n) to O(log n) in worst case.