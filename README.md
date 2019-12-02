# JavaScript Interview Questions and Answers

## 1. Explain event bubling
>https://www.sitepoint.com/event-bubbling-javascript/

## 2. What are JavaScript Data Types?
>**number** for numbers of any kind: integer or floating-point.
**string** for strings. A string may have one or more characters, there’s no separate single-character type.
**boolean** for true/false.
**null** for unknown values – a standalone type that has a single value null.
**undefined** for unassigned values – a standalone type that has a single value undefined.
**object** for more complex data structures.
**symbol** for unique identifiers.

## 3. What is hoisting?
> https://www.youtube.com/watch?v=mhZWi9tSy44

> Hoisting is JavaScript's default behavior of moving variable and function declarations to the top

#### Examples with variable hoisting

Example 1:
```javascript
// Because the variable "x" has not yet been defined, it produces an error
console.log(x); // Error
```

Example 2:
```javascript
// Even though we're console-logging the variable "x" before
// it is defined the var x declaration below gets hoisted to the top
console.log(x); // undefined
var x;

// so it actually behaves like this:

var x;
console.log(x); // undefined

// and that's why in this (second) example an "x" is undefined and
// does not produce an error
```

#### Examples with function hoisting
Example 1:
```javascript
// In this example we have function declaration that gets hoisted
// so we can call the function before it is technically defined
hoistedFunctionDeclaration(); // true

// This function is hoisted
function hoistedFunctionDeclaration() {
  return true;
}
```

Example 2:
```javascript
// In this example we have a function expression which does not
// get hoisted so we cannot call function before it is defined
unhoistedFunctionExpression(); // Error

// This function is not hoisted
var unhoistedFunctionExpression = function () {
  return true;
}
```
## 4. What is a closure?
> https://www.youtube.com/watch?v=mhZWi9tSy44

>A closure is an inner function that has access to the outer, or enclosing, function's variables.

```javascript
// Here we have an outer, or enclosing, function named "outerFunction"
function outerFunction(name) {
  // and that outer function has a variable in it's local scope, and the variable is called "greeting"
  var greeting = 'Hello';

  // Also our inner function (called innerFunction) has access to the "greeting" variable,
  // so the inner function will console log the "greeting" variable and the name passed to the "outerFunction"
  function innerFunction() {
    console.log(greeting + ' ' + name);
  }

  return innerFunction; // The outer/enclosing returns the inner function
}

var sayHelloToJohn = outerFunction('John');
sayHelloToJohn(); // Hello John

var sayHelloToEmily = outerFunction('Emily');
sayHelloToEmily(); // Hello John

// So, basically, we don't need to redefine a new
// function for every new name that we want to say Hello to.
```

## 5. What is functional programming?
> https://youtu.be/mhZWi9tSy44?t=177

> Functional programming involves using pure functions that avoid: shared state, mutating data, and side-effects.
It is declarative<sup>(meaning?)</sup>, rather than imperative<sup>(meaning?)</sup>.

Example 1:
```javascript
// In this example, an object has state that is shared by two functions below,
// and the two functions below mutate the object itself which means that they
// also produce side effect.
// And since the functions use state that's outside of themselves what they
// return is pretty unpredictable
var obj = {
  x: 4;
}

var addOneByMutatingSharedStateAndProducingASideEffect = function () {
  obj.x = obj.x + 1;
}

var subtractOneByMutatingSharedStateAndProducingASideEffect = function() {
  obj.x = obj.x - 1;
}
```

Example 2:
```javascript
// In this example the object is not shared or mutated at all.
// The two functions below don't mutate the object but rather take the object
// as an argument, and then they make the copy of the object and then perform
// the operation on the copy of the object,
// So, unlike the first example we always know what the functions will return
// based on what we pass in.
var obj = {
  x: 4
};

var addOneFunctionally = function (obj) {
  var newObj = {
    x: obj.x
  };

  newObj.x = newObj.x + 1;

  return newObj;
}

var subtractOneFunctionally = function (obj) {
  var newObj = {
    x: obj.x
  };

  newObj.x = newObj.x - 1;

  return newObj;
}
```

## What is the difference between synchronous and asynchronous code?
>https://youtu.be/mhZWi9tSy44?t=234

> Synchronous code is blocking - must complete before anything else can happen.
>Asynchronous code is not blocking - things can move on while we wait for something to finish.
>(Asynchronous JavaScript utilises Callbacks to do this. Asynchronous code is faster and allows for a better user experience because we don't need to wait for things to finish before we can move on, instead we can just move on and let things finish and then we can do what we need)

Example 1:
```javascript
// In this example, the three lines of code run in order - the next line cannot run unless the one before it completes.
console.log('One');
console.log('Two');
console.log('Three');
```

Example 2:
```javascript
// In this example we see that "Tree" is logged before "Two", even though "Two" shows up earlier in the code
// This is because setTimeout is asynchronous operation (it waits for the amount of time that we specified
// before running the function inside of it).
// The inner function is called the Callback, because it is called later when things are ready.
console.log('One');
setTimeout(function () {
  console.log('Two');
}, 1000);
console.log('Three');
```

## How can you determine if something is an array?
> https://youtu.be/mhZWi9tSy44?t=295

```javascript

```

:sparkles:
:+1:
  :evergreen_tree: