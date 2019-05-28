### Spring JDBC Exception Translator ###

**Custom Exception Translator**

![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbc-custom-exception.PNG)

In H2 database "23505" is the sql error code for primary key violation exception. Since we configured that if error code "23505" occurs, it will convert it to DataIntegrityViolation exception.

**Exception Translator Config**

![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbc-custom-exception-config.PNG)
