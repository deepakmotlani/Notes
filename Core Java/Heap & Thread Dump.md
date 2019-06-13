## Java Heap Dump
It is a snapshot of all the objects in the memory at any given point of time. These help us troubleshooting memory
leak issues. Heap dump are usually stored in binary format .hprof files. We can analyse this in tools like JVisualVM etc.

![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/heap-dump.PNG)

**What is Java memory leak?**
When certain objects are not used by application any more but it is not identified by garbage collector as unused.
As a result objects remain in memory indefinitely reducing the memory available to application.

**How to identify memory leaks**
* File/Text buffers not closed.
* Using HashMap with the key's class not implementing equals() & hashCode() method. No 2 objects will be same ever
	as we are not implementing equals method & hashmap will grow huge in size.
* Unwanted static variables in class.

**Ways to generate heap dumps** - JDK comes with several tools to capture heap dump, all of which are located in 
JDK bin directory.
* jmap
* jcmd
* JVisualVM - its a tool with GUI that lets us monitor

All these tools are manual, if you want to automatically capture the heap dump when an OutOfMemoryError occurs, you 
can do so by specifying following command line option. 

> java -XX:+HeapDumpOnOutOfMemoryError

And this has no overhead, so it is recommended to use this.

## Java Thread Dump
Since our applications are multi-threaded & if there are working on shared resources, contention b/w threads can
occur. Thread Dump is used to analyze thread contention & it proides exact status of each thread & its call stack.

We can generate this using multiple ways, 1 of them is JVisualVM.

![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/thread-dump.PNG)
