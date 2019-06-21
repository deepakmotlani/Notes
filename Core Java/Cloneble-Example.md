**Below program gives compile time error that clone method not visible, because clone is protected in Object class.
So we must override it to make it visible**
```
public class ClonebleTest {

	public static class Employee {
		private int id;
		private String name;
		
		public int getId() {
			return id;
		}
		public void setId(int id) {
			this.id = id;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
	}
	
	public static void main(String[] args) {
		ClonebleTest.Employee employee = new ClonebleTest.Employee();
		
		ClonebleTest.Employee employeeCopy = (ClonebleTest.Employee) employee.clone(); 
	}
}
```

**Next - if you override clone method in your class, compile time error would go away, but when you run the program
you will get CloneNotSupportedException, because your class is not implementin Cloneable iterface.**

**Next - you override clone method(simply call super.clone()) & implement Cloneable interface, code will run fine &
create a Shallow Copy of your object**

```
public class ClonebleTest {

	public static class Employee implements Cloneable {
		private int id;
		private String name;
		
		public int getId() {
			return id;
		}
		public void setId(int id) {
			this.id = id;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		
		public Object clone() throws CloneNotSupportedException {
			return super.clone();
		}
	}
	
	public static void main(String[] args) {
		ClonebleTest.Employee employee = new ClonebleTest.Employee();
		employee.setId(1);
		employee.setName("Deepak");
		
		try {
			ClonebleTest.Employee employeeCopy = (ClonebleTest.Employee) employee.clone();
			
			System.out.println("id: " + employeeCopy.getId() + " name: " + employeeCopy.getName());
			
			System.out.println(employee == employeeCopy);
		} catch (CloneNotSupportedException e) {
			e.printStackTrace();
		} 
	}
}
```

Output
```
id: 1 name: Deepak
false
```

**Next - lets add an object of Date in our class & see that clone method will not create separate copy of Date object
. Cloned object will also point to same Date object as orignial object. This is called Shallow Cloning**

```
public class ClonebleTest {

	public static class Employee implements Cloneable {
		private int id;
		private String name;
		private Date date;
		
		public int getId() {
			return id;
		}
		public void setId(int id) {
			this.id = id;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public Date getDate() {
			return date;
		}
		public void setDate(Date date) {
			this.date = date;
		}
		public Object clone() throws CloneNotSupportedException {
			return super.clone();
		}
	}
	
	public static void main(String[] args) {
		ClonebleTest.Employee employee = new ClonebleTest.Employee();
		employee.setId(1);
		employee.setName("Deepak");
		employee.setDate(new Date());
		
		try {
			ClonebleTest.Employee employeeCopy = (ClonebleTest.Employee) employee.clone();
			
			System.out.println("id: " + employeeCopy.getId() + " name: " + employeeCopy.getName() + " date: " + employeeCopy.getDate());
			
			System.out.println(employee == employeeCopy);
			System.out.println(employee.getDate() == employeeCopy.getDate());
		} catch (CloneNotSupportedException e) {
			e.printStackTrace();
		} 
	}
}
```

Output
```
id: 1 name: Deepak date: Fri Jun 21 11:57:05 IST 2019
false
true
```

**Next if you want Deep Cloning i.e. separate object of Date also then you need to override the clone method &
create your new Date objects & assign it.**