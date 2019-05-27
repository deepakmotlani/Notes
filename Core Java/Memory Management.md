## Memory Management

First thing, developers don't manage the memory explictly in Java, it is all taken care internally by Java. Java has 
automatic memory management, which runs garbage collector in b/g to cleanup unused objects. Though process is automatic
it doesn't guarantee anything. So knowing this is important, as it gives you advantage of writing high-performance &
optimized programs that will never crash with an OutOfMemory error.

![Java Memory]()

**Generally memory is divided in 2 main parts**
1. Stack
2. Heap