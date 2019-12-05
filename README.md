# JavaScript Interview Questions and Answers

## 1. Explain event bubling
>https://www.sitepoint.com/event-bubbling-javascript/

## 2. What are JavaScript Data Types?
>**number** for numbers of any kind: integer or floating-point.
>**string** for strings. A string may have one or more characters, there’s no separate single-character type.
>**boolean** for true/false.
>**null** for unknown values – a standalone type that has a single value null.
>**undefined** for unassigned values – a standalone type that has a single value undefined.
>**object** for more complex data structures.
>**symbol** for unique identifiers.

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
  // and that outer function has a variable in it's local scope, and the variable is called
  // "greeting"
  var greeting = 'Hello';

  // Also our inner function (called innerFunction) has access to the "greeting" variable,
  // so the inner function will console log the "greeting" variable and the name passed to
  // the "outerFunction"
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
// In this example, the three lines of code run in order - the next line cannot run unless the
// one before it completes.
console.log('One');
console.log('Two');
console.log('Three');
```

Example 2:
```javascript
// In this example we see that "Tree" is logged before "Two", even though "Two" shows up earlier
// in the code. This is because setTimeout is asynchronous operation (it waits for the amount of
// time that we specified before running the function inside of it).
// The inner function is called the Callback, because it is called later when things are ready.
console.log('One');
setTimeout(function () {
  console.log('Two');
}, 1000);
console.log('Three');
```

## How can you determine if something is an array?
> https://youtu.be/mhZWi9tSy44?t=295

If we do
```javascript
typeof []; // 'object'
```
we get an object, so that doesn't work

Instead we can use the constructor property to solve this problem, so if we do
```javascript
[].constructor; // Array
```
we get the global Array constructor, so we can do

```javascript
[].constructor === Array // true
```

## What is a higher order function?
> https://youtu.be/mhZWi9tSy44?t=320

> A higher order function is a function that can take another function as an argument or that returns a function as a result
> Notice: A closure is a kind of a higher order function

Example (this example basically implements the native forEach method for arrays)
```javascript
var forEach = function(array, iterator) {
  for(var i = 0; i < array.length; i++) {
    iterator(array[i], i);
  }
}

forEach(['Michael', 'Tim'], function(arrayItem, index) {
  console.log(arrayItem, index);
});
```
## What is the difference between an array and an array-like object?
> https://youtu.be/mhZWi9tSy44?t=374

> An array-like object does not have a standard array methods, but an array can be created from it with array.from

Example 1
```javascript
function arrayLikeExample(firstArgument, secondArgument) {
  arguments.forEach(function(argument) { // arguments variable is an array-like object(!)
    console.log(argument);               // and when we're using a forEach method, which is available (used) for arrays
  }); // Error                           // we get an Error
}

arrayLikeExample('first', 'second');
```

Example 2
```javascript
function arrayExample(firstArgument, secondArgument) {
  var arrayFromArguments = Array.from(arguments); // Here we create an actual array from an array-like variable

  arrayFromArguments.forEach(function(argument) {
    console.log(argument);
  }); // first, second
}

arrayExample('first', 'second');
```

## What is type coercion?
> https://youtu.be/mhZWi9tSy44?t=402

JavaScript sometimes allows something of a particular type to be coerced into another type.
Here are some examples:

```javascript
console.log('Hello ' + 8); // Here 8 is a number, but it is coerced into a string, so
                           // there is no type error that results

console.log('8' == 8); // Here, the first 8 is a string, and the second 8 is a number
                       // but they are counted as equal to one another because of
                       // the coercion
```

## What is the difference between two-way data binding and one-way data flow?
> https://youtu.be/mhZWi9tSy44?t=437

Two way data binding means that fields, such as inputs in the UI are bound to the model data, such that when either the UI or the model data changes the other one is also updated with it.
Two way data binding can cause side effects, that are difficult to debug. <span style="color:red; font-weight:bold">What side effects??!</span>

One way data flow means that there is a single source of truth (<span style="color:red; font-weight:bold">What is the single source of truth? Definition/explanation!</span>) and changes in that single source of truth can only flow in one direction.
With one way data flow it is easier to understand what is happening with the data, and therefore easier to debug. React/Redux is a good example of a pattern that uses one-way data flow.
:sparkles:
:+1:
  :evergreen_tree: