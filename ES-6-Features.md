## Features of ES6

* **Constants**, using this you can create immutable variables, meaning once value is assigned can't be changed.
  ```
    const a = 5;
  ```
* **Block Scoped Variables**
  ```
    for(let i = 0; i < 5; i++){
      console.log(i);
    }
  ```
* **Arrow Functions**
  ```
    const add = (num1, num2) => num1 + num2;
    const add = (num1, num2) => {
      console.log('num1: ' + num1);
      console.log('num2: ' + num2);
      return num1 + num2;
    };
  ```
  
* **Rest Parameter**
    ```
      function add(num1, num2, ...a) {
        return console.log(a.length);
      }
      
      add(1, 2, 3, 4, 5, 6); // in this case 1 is assigned to num1, 2 is assigned to num2, 
      //all the other params are assigned to 'a', i.e. a becomes an array of 3, 4, 5, 6
    ```
 * **Spread Operator**
    ```
      const a = {b:1, c:2};
      const d = {e:5, ...a}
      so value of d is {b:1, c:2, e:5}
    ```
[Find many more features here](http://es6-features.org/#GeneratorFunctionIteratorProtocol)
