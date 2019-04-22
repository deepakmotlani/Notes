**Steps to run the db queries & get the results from db**
* Load the driver class using Class.forName
* Create the connection using, DriverManager.getConnection(String url, String userId, String password)
* Create a statement using, con.createStatement()
* Execute the statement i.e. statement.executeQuery('SELECT * FROM EMPLOYEE'); which gives us a result set
* Iterate the result set to get the results
* Closing the connection.

**Types of statement**
* Statement is used when we have static query
* CallableStatement is used to run stored procedures & functions.
* PreparedStatement is used to execute parameterized query

**Advantages of PreparedStatement over Statement**
* PS is used to execute dynamic query, S is used to execute static query.
* PS is faster then S, as PS is complied only once at compile time, in case of S query is compiled every time it is executed

**Diff b/w execute, executeQuery & executeUpdate methods**
* e can be used to run both select & update queries, eQ can be used to run only select queries, eU can be used 
	to run only update/insert/delete queries
* e method returns a boolean type value where true indicates that ResultSet is returned, which can be later 
	retrieved & false indicates that integer or void is returned. eQ method returns ResultSet. eU method 
	returns integer value representing number of records affected.
		
**Diff b/w ResultSet & RowSet**
* ResultSet cannot be serialized as it maintains the connection with the database. RowSet is disconnected from 
	the database and can be serialized.
* ResultSet object is not a JavaBean object. RowSet Object is a JavaBean object.
* ResultSet is returned by the executeQuery() method of Statement Interface. Rowset Interface extends 
	ResultSet Interface and returned by calling the RowSetProvider.newFactory().createJdbcRowSet() method.
* ResultSet object is non-scrollable and non-updatable by default. RowSet object is scrollable and updatable 
	by default.

**How can we read & write images in db**
We can do this using blog type & using preparedStatement to store & retrieve it. We can associate an image 
with FileInputStream & associate this fileInputStream with preparedStatement. Similarly we can use resultSet to
read the blob data & write it to fileOutputStream
	
**Stored procedures are used to perform business logic while Functions are used to perform calculation. 
	SP can return 0 or more values while F can return only 1 value.**
