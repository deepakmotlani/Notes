## What does Spring JDBC does ##
![Spring JDBC](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20JDBC/images/spring-jdbc-does-what.PNG)


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
![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20JDBC/images/jdbctemplate-ex1.PNG)


Query to bind a variable
![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20JDBC/images/jdbctemplate-ex2.PNG)


Query for string

![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20JDBC/images/jdbctemplate-ex3.PNG)


Query for populating multiple domain objects
![](https://github.com/deepakmotlani/Notes/blob/master/Spring%20Framework/Spring%20JDBC/images/jdbctemplate-ex4.PNG)


**NamedParameterJdbcTemplate** class adds support for using named parameters instead of class placeholder '?'. You can pass all your query parameters in the form of a Map. You can also use **SqlParameterSource** to pass parameters to NamedParameterJdbcTemplate, where keys are the parameter names & values are parameter values.

We can retrieve auto-generated keys i.e. primary keys using **GeneratedKeyHolder**

## Important Points to remember
1. You should always use connection pools to get the database connection object instead of directly getting database connection. Advantage of doing so is that we can make sure that we are opening connections upto certain limit.
2. If we try to open more than specicified number of connections from database, it will start throwing exceptions.
3. You should have interface implementation for DAO so that if underlying technique i.e. JDBC, Hiberante etc. get changed, it should not impact callers. Also we should use modal objects in method signatures of DAO, instead of individual parameters i.e. id, name, email etc.

**We can use following Datasource implementations are available** -
1. Apache gave BasicDataSource. 
   While creating BasicDataSource object we can set url, password, driver, maximum number of connections, max idle time etc. This internally creates datasource pool & keeps maximum number of connections & we can get connection from connection pool. Then you can get connections from basicDataSource using getConnection method.
2. Mchance gave ComboPooledDataSource.
3. Spring gave DriverManagerDataSource.
4. WebLogic gave WebLogicDataSource. 
& many many more implementations are available.

**Internally connection pool maintain 2 maps used & unused connections, when you call get connection method, it is placed in used map, when you close the connection it will put it in unused connections & it doesn't actually returns to database, it is just returned to connection pool. Connection Pool creates all the connections at application startup & releases them at application shutdown.**

**So it is recommended to use datasources to get database connections instead of directly opening connections.**

We can create Jdbc Template class object by using datasource, Jdbc Template has a setter method for datasource. JdbcTemplate methods internally manages opening & closing connection.

**Difference b/w Plain JDBC & Spring JDBC**

| Plain JDBC | Spring JDBC |
| ---------- | ----------- |
| It throws compile time exceptions i.e. SQL exceptions | It throws runtime exception i.e. DataAccess exceptions |
| Developer should close connections | Developer don't have to close connections |
| For all operations this returns resultset, we have to iterate resultset to get data | This provides various generic methods for ex: queryForInt to get integer data|
