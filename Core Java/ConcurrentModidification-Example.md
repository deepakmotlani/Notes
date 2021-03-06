**First Approach - Plain for loop which uses index to access elements, works fine.**
```
public static void main(String[] args) {
	List<Integer> integers = new ArrayList<Integer>();
	integers.add(1);
	integers.add(2);
	integers.add(3);
	integers.add(4);
	
	for(int i = 0; i < integers.size(); i++) {
		if(integers.get(i) == 1) {
			System.out.print("Removing");
			integers.remove(i);
		}
	}
	System.out.print(integers);
}
```

**Second Approach - Enhanced for loop which uses index to access elements, throws ConcurrentModificationException.**
```
public static void main(String[] args) {
	List<Integer> integers = new ArrayList<Integer>();
	integers.add(1);
	integers.add(2);
	integers.add(3);
	integers.add(4);
	
	integers.forEach(i -> {
		if(i == 4) {
			integers.remove(integers.indexOf(i));
		}
	});
}
```

**Third Approach - Enhanced for loop which uses iterator to remove elements, works fine.**
```
public static void main(String[] args) {
	List<Integer> integers = new ArrayList<Integer>();
	integers.add(1);
	integers.add(2);
	integers.add(3);
	integers.add(4);
	
	Iterator<Integer> iterator = integers.iterator();
	while(iterator.hasNext()) {
		int i = iterator.next();
		if(i == 1) {
			iterator.remove();
		}
	}
	System.out.print(integers);
}
```

**Fourth Approach - Stream API for looping which index to remove, throws ConcurrentModificationException.**
```
public static void main(String[] args) {
	List<Integer> integers = new ArrayList<Integer>();
	integers.add(1);
	integers.add(2);
	integers.add(3);
	integers.add(4);
	
	integers.stream().forEach(i -> {
		
		if(i != null && i == 1) {				
			integers.remove(0);
		}			
	});
	System.out.print(integers);
}
```

**Why iterator.remove() doesn't throw exception, but list.remove() does throw is because, iterator maintains a data structure internally (or may be can say a copy of collection), whenever you perform any operation on iterator it matches the internal state with the actual state of collection, if it doesn't match it throws ConcurrentModificationException, but if you use iterator.remove() it will update the internal state of collection as well as the original collection, that's why it doesn't throw exception**
