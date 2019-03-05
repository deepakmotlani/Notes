### Features

1. **forEach()** method is a default method in Iterable interface. From Java 8, interfaces are enhanced to have method with implementation. forEach method takes **Consumer** object as areguement.

![For Each](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/for-each.PNG)

2. We can use **default** & **static** keyword to create interfaces with method implementation. 
Static methods are available only through & inside the interface. It can't be overridden by an implementing class.

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/interface-static-method.PNG)

To call it out side the interface, standard approach would be

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/interface-static-method-usage.PNG)

Output would be

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/interface-static-method-usage-result.PNG)

Default Method Example

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/interface-default-method.PNG)

Usage

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/interface-default-method-usage.PNG)

Result

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/interface-default-method-usage-result.PNG)
