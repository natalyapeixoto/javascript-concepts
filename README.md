## JavaScript concepts


### Closure

A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, *a closure gives you access to an outer function's scope from an inner function*. In JavaScript, closures are created every time a function is created, at function creation time.


#### Lexical Scope:

~~~javascript
function init() {
  var name = 'Mozilla'; // name is a local variable created by init
  function displayName() { // displayName() is the inner function, a closure
    console.log(name); // use variable declared in the parent function
  }
  displayName();
}
init();
~~~ 

Inner functions have access to the variables of outer functions, displayName() can access the variable name declared in the parent function, init().

#### Closure:

~~~javascript
function makeFunc() {
  var name = 'Mozilla';
  function displayName() {
    console.log(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
~~~ 

At first glance, it might seem unintuitive that this code still works. In some programming languages, the local variables within a function exist for just the duration of that function's execution. Once makeFunc() finishes executing, you might expect that the name variable would no longer be accessible. However, because the code still works as expected, this is obviously not the case in JavaScript.

The reason is that *functions in JavaScript form closures*. A closure is the combination of a function and the lexical environment within which that function was declared. This environment consists of any local variables that were in-scope at the time the closure was created. In this case, myFunc is a reference to the instance of the function displayName that is created when makeFunc is run. The instance of displayName maintains a reference to its lexical environment, within which the variable name exists. For this reason, *when myFunc is invoked, the variable name remains available for use, and "Mozilla" is passed to console.log*.

#### More complex closure example:

~~~javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // can you guess what will be printed?
console.log(add10(2)); // ?
~~~


### Hoisting 

When the JavaScript engine executes the JavaScript code, it creates the global execution context. The global execution context has two phases: creation and execution.
During the creation phase, the *JavaScript engine moves the variable and function declarations to the top of your code*. This feature is known as hoisting in JavaScript.

#### Variable hoisting

~~~javascript
console.log(counter); // undefined
var counter = 1;
~~~ 

Technically, the code looks like the following in the execution phase:
~~~javascript
var counter;

console.log(counter); // undefined
counter = 1;
~~~

That does not happen with `const` nor `let`:
~~~javascript
console.log(counter);
let counter = 1;
~~~
with the code above we get the following error: `"ReferenceError: Cannot access 'counter' before initialization`

#### Function Hoisting 

~~~javascript
addTwo(5) // 7  

function addTwo(b) {
    return b + 2
}
~~~
In this example, *we called the addTwo() function before defining it* and the code still works. 

#### Function Expressions 
~~~javascript
let x = 20,
    y = 10;

let result = add(x,y);
console.log(result);

var add = function(x, y) {
return x + y;
}
~~~
Executing this code we get: `"TypeError: add is not a function`

During the creation phase of the global execution context, the JavaScript engine creates the add variable in the memory and initializes its value to undefined.

When executing the following code, the add is undefined, hence, it isn’t a function:

let result = add(x,y);
Code language: JavaScript (javascript)
The add variable is assigned to an anonymous function only during the execution phase of the global execution context.

If add was an *arrow function* like 
~~~javascript
var add = (x, y) => x + y;
~~~
The code also issues the same error as the function expression example because *arrow functions are syntactic sugar for defining function expressions*.


### Arrow functions

~~~javascript
const sum = (a, b) => a + b //arrow function

//what this is actually doing:

const sum = function(a, b) {
    return a + b
}
// the arrow function created a function expression. 
~~~

##### Arrow Function implicity return:
~~~javascript
const sum = (a, b) => a + b  // this arrow function has an implicity return 
const sum = (a, b) => {
    return a + b 
} // this does not 

// implicity return is just a sintax sugar for simplicity. 
~~~

Arrow functions have a lexical return
Arrow functions are sintax sugar for function expressions
Arrow functions are a ES6 feature 
Arrow function do not hoist


### ES6 
coming soon...