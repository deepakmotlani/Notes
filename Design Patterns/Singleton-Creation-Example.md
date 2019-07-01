## Singleton

**Ways of creating singleton instances in Java**

* Eager initialization, with private constructor
```
public class Singleton {
	private static Singleton singleton = new Singleton();
	
	private Singleton() {
		
	}
	
	public static Singleton getInstance() {		
		return singleton;
	}
}
```

* Static Block initialization, with private constructor, it is mostly similar to eager initialization, just that
	in static blocks, we can handle exceptions if any.
```
public class Singleton {
	private static Singleton singleton = null;
	
	private Singleton() {
		
	}
	
	static {
		try {
			singleton = new Singleton();
		}
		catch(Exception exception) {
			exception.printStackTrace();
		}
	}
	
	public static Singleton getInstance() {		
		return singleton;
	}
}
```

* Lazy Initialization with private constructor

```
public class Singleton {
	private static Singleton singleton = null;
	
	private Singleton() {
		
	}
		
	public static Singleton getInstance() {
		if(singleton == null) {
			singleton = new Singleton();
		}
		return singleton;
	}
}
```

* Thread Safe Singleton, using synchronized
```
public class Singleton {
	private static Singleton singleton = null;
	
	private Singleton() {
		
	}
		
	public static synchronized Singleton getInstance() {
		if(singleton == null) {
			singleton = new Singleton();
		}
		return singleton;
	}
}
```

* Bill Pugh Singleton implementation, which uses static inner class & doesn't require synchronized, static inner 
	class is loaded only when getInstance method is called.
```
public class Singleton {	
	private Singleton() {
		
	}
	
	private static class InnerSingleton {
		private static Singleton INSTANCE = new Singleton();
	}
		
	public static synchronized Singleton getInstance() {
		return InnerSingleton.INSTANCE;
	}
}
```

## Breaking Singleton pattern using Java Reflection

```
public class SingletonMain {

	@SuppressWarnings("rawtypes")
	public static void main(String[] args) {
		Singleton singleton = Singleton.getInstance();
		Constructor[] constructors = Singleton.class.getDeclaredConstructors();
		for(Constructor constructor : constructors) {
			constructor.setAccessible(true);
			try {
				Singleton singleton1 = (Singleton) constructor.newInstance();
				
				System.out.println(singleton == singleton1);
				break;
			} catch (InstantiationException | IllegalAccessException
					| IllegalArgumentException | InvocationTargetException e) { 
				e.printStackTrace();
			}
		}
	}
}
```
**Above problem can be solved using Enum, since Java ensures that any enum is instantiated only once in Java
program.**
```
enum Singleton {	
	INSTANCE;
	
	public static void doSomething() {
		
	}
}
```

## Singleton also breaks if we serialize & then deserialize the objects. In order to avoid that we should implement
the readResolve method as below

```
protected Object readResolve() {
	return getInstance();
}
```



