**Differences between HashMap and HashTable in Java.**
1. HashMap is non synchronized. It is not-thread safe and can’t be shared between many threads without proper synchronization code whereas Hashtable is synchronized. It is thread-safe and can be shared with many threads.
2. HashMap allows one null key and multiple null values whereas Hashtable doesn’t allow any null key or value.
3. HashMap is generally preferred over HashTable if thread synchronization is not needed

**What is the final blank variable?**<br/>
A final variable, not initialized at the time of declaration, is known as the final blank variable. We can't initialize the final blank variable directly. Instead, we have to initialize it by using the class constructor. It is useful in the case when the user has some data which must not be changed by others, for example, PAN Number. 

**Can we initialize the final blank variable?**<br/>
Yes, if it is not static, we can initialize it in the constructor. If it is static blank final variable, it can be initialized only in the static block.

**Can we declare a constructor as final?**<br/>
The constructor can never be declared as final because it is never inherited. Constructors are not ordinary methods; therefore, there is no sense to declare constructors as final. However, if you try to do so, The compiler will throw an error.

**Can you achieve Runtime Polymorphism by data members?**<br/>
No, because method overriding is used to achieve runtime polymorphism and data members cannot be overridden. We can override the member functions but not the data members. Consider the below example<br/>
>class Bike{  
  >int speedlimit=90;  
>}  
>class Honda3 extends Bike{  
  >int speedlimit=150;  
  >public static void main(String args[]){  
  >Bike obj=new Honda3();  
  >System.out.println(obj.speedlimit);//90  
   }  
>}
>Output is 90

**Find Here**
* https://www.javatpoint.com/corejava-interview-questions

How Hashmap works - https://www.geeksforgeeks.org/internal-working-of-hashmap-java/

**Why is String class immutable in Java**?
Because String are stored in String constant pool which may be shared b/w multiple clients, so if 1 client change the value of String, then it may impact other clients as well.
