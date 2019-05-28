![Exception Handler](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20MVC/images/mvc-exception-handler.PNG)

Above configuration is used to configure Exception Pages for any exception in the system. In this case we have configured CustomExceptionPage.jsp for com.deepak.exception.CustomException.
And error.jsp for all other exceptions.

And in my controller I simply throw CustomException -

![Controller](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20MVC/images/mvc-exception-handler-throw.PNG)

Similar thing can be acheived through **@ExceptionHandler**

![Annotation Based](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20MVC/images/mvc-exception-handler-annotation.PNG)

**@ControllerAdvice** is used, so that we can extract all the exception handlers in a separate class.

For @ExceptionHandler to work \<mvc:annotation-driven\/> is mandatory.
