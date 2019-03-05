
### Functional Interfaces

are gathered in java.uitl.function package, satisfy most developers needs. Interfaces with only 1 abstract method act as functional interfaces.

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/functional-interface.PNG)

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/functional-interface-definition.PNG)

We can also remove the Foo interface completely & write our code like below

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/functional-interface-without-interface.PNG)

Annotate methods with @FunctionalInterface, at first, this annotation seems to be useless. Even without it, your interface will be treated as functional as long as its has just 1 abstract method. But using **@FunctionalInterface**, the compiler will trigger an error in response to any attempt to break the predefnied structure. It makes easier to understand for developers.

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/functional-interface-annotated.PNG)

We can also add default methods to Functional Interface.

**Example code for comparing age & sorting**

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/example-1-normal-java-code.PNG)

Since Comparator is a functional interface, we can also write it using lambda expression

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/example-1-using-lambda.PNG)

Since we already have method to compare age, we can use **method reference i.e. ::** also like below

![](https://github.com/deepakmotlani/Notes/blob/master/Java-8/images/example-1-using-method-ref.PNG)
