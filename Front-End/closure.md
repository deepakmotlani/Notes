## Closures

Java script can be local(inside function) or global(window object) scope.

Global variables can be made private with closures, which are not in window scope.

A function can access all the variables inside the function as well as global variables.

Local variables can heve their lifetime only till function, as soon as function completes the variables will be lost.

Suppose you want a counter variable to be incremented on every function invocation. So you can keep a global variable
& on increment function you can increment it. But the problem is that anyone else can change this global variable.

How to solve this problem, Java script inner function can solve this problem, so we need closure.

**Closure is a self invoking function, which runs only once & sets the counter to 0 & returns a function.**

In the below expression, self invoking function executes & sets the counter to 0 & returns a function which gets 
assigned to increment variable.

var increment = (function() {
	var counter = 0;
	
	return function() {
		return ++counter;
	}
})();

on every call to increment, you get the incremented counter.
increment(); //1
increment(); //2
increment(); //3
