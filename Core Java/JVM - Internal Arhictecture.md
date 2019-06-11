## JVM Internal Architecture

![](https://github.com/deepakmotlani/Notes/blob/master/Core%20Java/images/JVM-Architecture.png)

### Class Loader SubSystem
It is responsible for mainly 3 activities -
* Loading
* Linking
* Initialization


**Loading** - Class Loader reads .class file, generates corresponding binary data & save it in method area. For each
.class file, JVM stores following info in method area.

* Fully qualified name of loaded class & its immediate parent class
* Whether .class is related to Class/Interface/Enum.
* Modifier, variables & method information etc.

After loading the .class file, JVM creates object of Class class to represent this file in heap. For every .class file
, only object of Class class is created.

There are 3 kinds of Loaders -
* **Bootstrap Class Loader** - Every JVM must have a bootstrap class loader, capable of loading trusted classes. It 
	loads Core Java API classes present in JAVA_HOME/jre/lib.
* **Extension Class Loader** - It is child of bootstrap loader & it loads classes from JAVA_HOME/jre/lib/ext.
* **System/Application Class Loader** - It is child of extenstion class loader & is responsible for loading classes
	from application class path.
	
**JVM follows delegation-hierarchy for loading classes. Application Class Loader delegeates to Extension which in 
	turn delegates to Bootstrap class loader. If the class is found on bootstrap path it is loaded, otherwise
	request is given back to Extension class loader & finally back to System/Application class loader. At last if
	system doesn't find the class, it throws ClassNotFoundException.**