A new **java.util.stream** has been added in Java 8 to perform filter/map/reduce like operations with the collection. Stream API will allow sequential as well as parallel execution. This is one of the best feature.

**Stream has following intermediate & terminal operations**
* Intermediate Operations
	* map: The map method is used to map the items in the collection to other objects according to the Predicate passed as argument.
	
		List square = number.stream().map(x->x*x).collect(Collectors.toList());

See more from here https://www.geeksforgeeks.org/stream-in-java/

Collection interface has been extended with **stream()** and **parallelStream()** default methods to get the Stream for sequential and parallel execution. Let’s see their usage with simple example

```
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

public class StreamExample {

	public static void main(String[] args) {
		
		List<Integer> myList = new ArrayList<>();
		for(int i=0; i<100; i++) myList.add(i);
		
		//sequential stream
		Stream<Integer> sequentialStream = myList.stream();
		
		//parallel stream
		Stream<Integer> parallelStream = myList.parallelStream();
		
		//using lambda with Stream API, filter example
		Stream<Integer> highNums = parallelStream.filter(p -> p > 90);
		//using lambda in forEach
		highNums.forEach(p -> System.out.println("High Nums parallel="+p));
		
		Stream<Integer> highNumsSeq = sequentialStream.filter(p -> p > 90);
		highNumsSeq.forEach(p -> System.out.println("High Nums sequential="+p));

	}
}

Output
High Nums parallel=91
High Nums parallel=96
High Nums parallel=93
High Nums parallel=98
High Nums parallel=94
High Nums parallel=95
High Nums parallel=97
High Nums parallel=92
High Nums parallel=99
High Nums sequential=91
High Nums sequential=92
High Nums sequential=93
High Nums sequential=94
High Nums sequential=95
High Nums sequential=96
High Nums sequential=97
High Nums sequential=98
High Nums sequential=99

```
