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
