## Memory Management

First thing, developers don't manage the memory explictly in Java, it is all taken care internally by Java. Java has 
automatic memory management, which runs garbage collector in b/g to cleanup unused objects. Though process is automatic
it doesn't guarantee anything. So knowing this is important, as it gives you advantage of writing high-performance &
optimized programs that will never crash with an OutOfMemory error.

![Java Memory](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/java-memory-1.jpg)

**Generally memory is divided in 2 main parts**
1. Stack
2. Heap

**Stack** is responsible for holding 
1. references to objects in heap
2. primitives, which holds value itself rather than a reference

Variables on stack have certain visibility associated, also called **scope**. Let's say there is a method which is 
being executed has some local variables, so the compiler can access only those local variables(assuming that there
are no global variables), when executing this method. Once method completes, top of stack pops out & active scope 
changes.

Notice in the picture above that there are **multiple stack memory**, this is because oof multiple threads being executed.
**Each thread in java has its own Stack memory & it can't access other Thread's stack.**

**Heap** is the part of memory which stores actual object, which are refered from references in stack.

```
StringBuilder stringBuilder = new StringBuilder();
```

**new** keyword here is reponsible for ensuring that there is enough free space in heap & creating the object in heap &
referring it via stringBuilder reference, which goes to stack.

**There exists only 1 heap memory per JVM & is shared b/w multiple threads.** 

If we look at the picture closely, we will see that there are different kind of references to objects of heap. This is
because we have different types of references i.e. **strong**, **weak**, **soft** & **phantom** references.

1. **Strong Reference** - In the example above stringBuilder reference has a Strong reference to object in heap. 
Object in heap can't be garabage collected while there is a strong reference to object.

2. **Weak Reference** - whenever we have a weak reference to an object, it is most likely to be garbage collected in
the next garbage collection process.

This is how we create it -
```
WeakReference<StringBuilder> reference = new WeakReference<>(new StringBuilder());
```

This is used mainly in caching scenarios, whenever you fetch the data from a source you keep a wek refernce for it,
because you think you may need it again but you don't know when will you need it again. So keeping this in weak 
reference makes sense. Good implementation for this is WeakHashMap, Entry class extends WeekReference.

```
private static class Entry<K,V> extends WeakReference<Object> implements Map.Entry<K,V> {
	V value;
}
```

Once a particular key is garabage collected, the entire object is garabage collected & entire entry is removed from 
map.

3. **Soft Reference** - These type is used for memory-sensetive scenarios, since these will be garbage collected only
when application is running low on memory. So until there is sufficient memory available GC will not touch soft refernce.
Java also guarantee that all soft references will be garbage collected before throwing OutOfMemory error.

```
SoftReference<StringBuilder> reference = new SoftReference<>(new StringBuilder());
```

4. **Phantom Reference** - tough to understand this.



