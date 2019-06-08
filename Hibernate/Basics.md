### Hibernate Config XML file
```
<hibernate-configuration>
    <session-factory>
        <!-- SQL Dialect -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
 
        <!-- Database Connection Settings -->
        <property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/tutorialDb</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password"></property>
        <property name="show_sql">true</property>
 
        <!-- Specifying Session Context -->
        <property name="hibernate.current_session_context_class">org.hibernate.context.internal.ThreadLocalSessionContext</property>
 
        <!-- Mapping With Model Class Containing Annotations -->
        <mapping class="com.jcg.hibernate.onetomany.mapping.Student" />
        <mapping class="com.jcg.hibernate.onetomany.mapping.MarksDetails" />
    </session-factory>
</hibernate-configuration>
```

### Hibernate Mapping file
```
<hibernate-mapping>
   <class name = "Employee" table = "EMPLOYEE">
      
      <meta attribute = "class-description">
         This class contains the employee detail. 
      </meta>
      
      <id name = "id" type = "int" column = "id">
         <generator class="native"/>
      </id>
      
      <property name = "firstName" column = "first_name" type = "string"/>
      <property name = "lastName" column = "last_name" type = "string"/>
      <property name = "salary" column = "salary" type = "int"/>
      
   </class>
</hibernate-mapping>
```

### Hibernate entities with annotation
```
@Entity
@Table
public class Project{

	@Id
	@GeneratedValue
	private int id;
	
	@Column(name = "projectName")
	private String name;
	
	@OneToMany(cascade = CascadeType.ALL, mappedBy = "project", fetch = FetchType.EAGER, orphanRemoval = true)
	private List<Employee> emloyees;	
}

@Entity
@Table
public class Employee{

	@Id
	private int id;
	
	@Column
	private String name;
		
	@ManyToOne
	@JoinColumn(name = "project")
	private Project project;	
}
```


### Annotations from javax.persistence
**@Entity** annotation marks this class as an entity.

**@Table** annotation specifies the table name where data of this entity is to be persisted. If you don't use @Table annotation, hibernate will use the class name as the table name by default.

**@Id** annotation marks the identifier for this entity.

**@GeneratedValue** instructs db to generate value for this column automatically.

**@Column** annotation specifies the details of the column for this property or field. If @Column annotation is not specified, property name will be used as the column name by default.

**@OneToMany** used to indicate 1:N from containing entity & field entity.
	cascade = CascadeType[], with possible values ALL, DETACH, MERGE, REMOVE, PERSIST, REFRESH
	fetch = whether association should be fetched lazily or eagerly
	mappedBy = field that owns relationship
	orphanRemoval = whether to delete the orpans

**@ManyToOne** used to indicate N:1 from containing entity & field entity. Or we can say this is used on foreign keys
	of entity. Genrally accompanied with @JoinColumn

**@JoinColumn** genrally use with @ManyToOne with name attribute indicating the name of column in table

**We should hibernateTemplate object to perform database transactions, we need to create the hibernateTemplate from sessionFactory, this hibernateTemplate object takes care of everything i.e. opening & closing connections. we simply write hibernateTemplate.save or update etc. Session Factory manages the pools of sessions internally. **
