## What does Spring JDBC does ##
![Spring JDBC](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/spring-jdbc-does-what.PNG)


### Approaches for database access ###
1. JdbcTemplate is classic Spring JDBC approach & is most popular.
2. NamedParameterJdbcTemplate wraps a JdbcTemplate to provide named parameters instead of traditional "?" placheloders.
3. SimpleJdbcInsert & SimpleJdbcCall optimize database metadata to limit the amount of necessary configuration.

### Package Hierarchy ###

Consists of four different packages namely **core, datasource, object & support.**

- **org.springframework.jdbc.core** package contains JdbcTemplate class & its various callback interfaces.

   - **org.springframework.jdbc.core.simple** package contains SimpleJdbcInsert & SimpleJdbcCall classes.

   - **org.springframework.jdbc.core.namedparam** package contains NamedParamtereJdbcTemplate class & related support classes.

**JdbcTemplate** class is the central class, it handles creation & release of resources. It performs basic tasks of the core JDBC workflow such as statement creation & execution. Jdbctemplate class executes SQL queries, update statements & stored proc call, performs iteration over ResultSets & extraction of returned parameter values. It also catches exceptions & translates them to generic, more informative exceptions. 

Here are some simple examples - 

Query for getting count
![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbctemplate-ex1.PNG)


Query to bind a variable
![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbctemplate-ex2.PNG)


Query for string

![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbctemplate-ex3.PNG)


Query for populating multiple domain objects
![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20JDBC/images/jdbctemplate-ex4.PNG)
