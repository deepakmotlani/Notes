## Spring Boot with JDBC ##

Adding a dependency **spring-boot-starter-jdbc** takes care of lot of things like, creating **jdbcTemplate** which can be directly used to insert or update data.

All you need to do is specify the database connection properties in the application.properties files starting with prefix **spring.datasource** like -

> spring.datasource.url=jdbc:h2:~/test

> spring.datasource.username=\<username\>

> spring.datasource.password=\<password\>

Now you can simply **autowire jdbcTemplate** object in the repository & it should be available for you to perform any transactions.


**If you want to create your **jdbcTemplate** & **dataSource**, you can use following configurations**

![JDBC Config](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbc-config.PNG)
