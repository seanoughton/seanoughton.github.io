---
layout: post
title:      "Scope, Context and Hoisting in Javascript"
date:       2018-08-06 22:31:36 +0000
permalink:  scope_context_and_hoisting_in_javascript
---


## Scope

In Javascript, Scope determines where variables are  accessible (visible). There are two types of scope: Global scope and Local scope.

### Global Scope

A variable declared outside a function or a block, becomes a Global variable .  A Global variable  is accessible throughout the Global Execution Context.  It therefore has Global scope.  

### Local Scope 

A Local Scope refers to any scope defined past the Global Scope.   Every function and/or block creates their own scope. Variables defined inside a function are not accessible (visible) from outside the function, and thus become local to the function. These variables are said to have function scope.  Any locally scoped items are not visible in the Global Scope, unless exposed by returning the variables in some way.

The one exception to this is if you assign a value to a variable that has not been declared, it will automatically become a Global variable.
Ex. 

`x = 0`  is a Global variable no matter where this code lives, either in the Global scope or in a function.

vs 

`let x = 0` is Global or local depending on where this code lives. It is local if it lives in a function or a block, otherwise it is Global.

**Nested Functions**
If a variable is defined inside of a function, it is visible everywhere inside that function, even inside other functions inside that function.  

**Lifespan**
Local variables have a  lifespan.   They are created when a function starts, and deleted when the function is completed. 

**Exceptions**
For/While Loops or expression statements like if or switch, do not create scope.   So a variable created with **var** inside a loop is accessible outside of that loop. Variables created with **let** or **const**, are not accessible outside that loop.


### Scope with Var vs Let/Const

The scope of a variable declared with the keyword **var** is its current execution context. This is either the enclosing function or for variables declared outside any function, the global context.  Variables declared with the keyword **let/const** are block scoped and not function scoped.  This means that the variable's scope is bound to the block in which it is declared and not the function in which it is declared.

```
function test () {
  { let a = "test" }
  console.log(a)
}
```

```
test() ; ReferenceError: a is not defined
    at test 
```

### Lexical Scope

Lexical scoping describes how the Javascript engine resolves variable names when functions are nested. It uses the location where a variable is declared to determine where that variable is available. Nested functions have access to variables declared in their outer scope. 

### Scope Chain

Continuing with the idea of lexical scope, is the concept of the Scope Chain. It's based upon the idea that nested functions have access to the scopes "above" them.  When the Javascript engine tries to find an identifier, it first looks to see if the identifier is defined in the the current scope, if it can’t find it in the current scope it moves out one level and looks for the identifier in the outer scope, and keeps moving out until it finds the identifier or reaches the outermost scope, the Global Scope.  If the Javascript engine looks in all of the functions and the Global Scope and cannot find the identifier, it will return an error.

## Context (**"This"**)

Every function invocation has both a scope and a context associated with it.  Scope has to do with what variables a function has access to when it is declared and invoked.  Whereas, context is always the value of the **"this"** keyword.  **"This"** is a reference to the object that “owns” the currently executing code. 

**"This"** references the current context in which it is invoked, either global scope, function scope, or class scope.  

For functions, the value of **"this"** is determined based on how the function is called.  When a function is called as a method of an object, **"this"** is set to the object the method is called on.  When creating an instance of an object with the **new** operator, **"this"** is set to the newly created instance.  When called as an unbound function, **"this"** will default to the Global context.

With arrow functions, the value of **"this"** is based on the function's surrounding context. In other words, the value of **"this"** inside an arrow function is the same as the value of **"this"** outside the function.


## Execution Context
In Javascript, one task is executed at a time in a specific Execution Context. Initially, the Execution Context is Global. However,  each function invocation will result in the creation of a new Execution Context.  The Execution Context is not a context in the sense of **"this"**, it is really more of an Execution Scope. It is the scope the current code is being evaluated in.

An Execution Context can be divided into a creation and execution phase. In the creation phase, the interpreter will first pre-process all the variables, function declarations, and arguments defined inside the Execution Context. From there the scope chain is initialized, and the value of **"this"** is determined. Then in the execution phase, code is interpreted and executed.

When a new function is invoked, JavaScript creates a new Execution Context, a local Execution Context. That local Execution Context will have its own set of variables, and these variables will be local to that Execution Context. 

Each time a new Execution Context is created it is placed at the top of the Execution Stack. The Execution Stack is a mechanism that keeps track of where the program is in its execution.  The browser will always execute the current Execution Context that is at the top the Execution Stack. 

When a function execution ends, the local Execution Context is removed from the Execution Stack and the function sends it's return value. Because that local Execution Context is no longer there, the variables that were declared within the local execution context are erased. They are no longer available. 


## Closures

**Definition**

In it's simplest form, a closure is a function bound up with all the variables that the function has access to when the function is declared.  These functions **close over** variables they need to operate. Therfore, a closure is a function with **state.**  Because it closes over these variables and encapsulates them,  it gives you access to an outer functions scope from an inner function.

Whenever you declare a new function and assign it to a variable, you store the function definition, as well as a Closure. The Closure contains all the variables that are in scope at the time of creation of the function.  Creating the Closure **vacuum's up** all of the variables needed for for the functions operation. The closure will then have access to these variables wherever it is used.

To use a Closure, simply define a function inside another function and expose it, that is, return it or pass it to another function.  Then when you execute functions, their closures enable them to access data in their scopes.  


Ex.

```
function createMultiplier(x) {
  return function(y) {
    return x * y;
  };
}
var mult5 = createMultiplier(5);
var mult10 = createMultiplier(10);
```

In essence, **createMultiplier** is a function factory. **mult5** and **mult10** are both Closures. They share the same function body definition, but store different lexical environments.  In **mult5**'s lexical environment, x is 5, while in the lexical environment for **mult10**, x is 10.

**Why Create Closures**

Closures are useful because they let you associate some data with a function that operates on that data.  This is similar to object-oriented programming, where objects allow us to associate some data with one or more methods. One example where you might want to use a closure would be where you attach a behavior to a DOM element, like a click event for a button.  The closure would be attached as a callback function, that is executed in response to the event.

From some research I did, it seems like Closures are a mechanism used to enable data privacy. The enclosed variables are only in scope within the containing function. You can’t get at the data from an outside scope except through the object’s privileged methods. 


**Closures and Scope**

Scopes have a lifetime. When you call a function, you create a scope during the execution of that function. Then that scope goes away. Unlike scopes, closures are created when you define a function, not when you execute it. Closures also don’t go away after you execute that function. You can access the data in a closure long after a function is defined and after it gets executed as well.  A closure is a function having access to the parent scope, even after the parent function has closed.



## Hoisting

**Definition**

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope (global or local) before code execution, now matter where they are declared.  In other words, a variable can be used before it has been declared and a function can be invoked before it is declared.

Example:

```
testHoisting()

function testHoisting() {
  let a = 1;
  console.log(a)
}
//Ouput : 1
```


**Declaration**
The JavaScript engine treats all variable declarations using “var” as if they are declared at the top of a functional scope(if declared inside a function) or global scope(if declared outside of a function) regardless of where the actual declaration occurs.  This occurs before the code is executed.

**Initialization**
JavaScript only hoists declarations, not initializations. So variable assignment remains in the same place and is not hoisted. 

The following will return undefined:

```
console.log(x)
var x = 5; // Initialize x
```

This is because only the declaration (var x), not the initialization (=5) is hoisted to the top.
Because of hoisting, x has been declared before it is used, but because initializations are not hoisted, the value of x is undefined.

Undeclared variables do not exist until code assigning them is executed. Therefore, assigning a value to an undeclared variable implicitly creates it as a global variable when the assignment is executed. This means that, all undeclared variables are global variables.

### Variables and constants declared with let or const vs var

Technically JavaScript hoists variables declared with let and const. However, they remain uninitialised at the beginning of execution, while variables declared with var are initialised with a value of undefined. Therefore, the interpreter throws an error if we use a let/const before declaring and initialising it. 

### Hoisting Functions

**Function declarations** are hoisted, so effectively the function itself is hoisted and you can invoke the function before it is declared.  

**Function expressions**, however are not hoisted. The function expression declaration is hoisted, but not the assignment.

Example:

`const myFunction = function () { 
/// code 
}`

myFunction is declared at the top by hoisting, but the function is not available until it is assigned. The Javascript interpreter sees the function expression declaration as just a variable and not a function until is assigned the function.


### Hoisting Order of Precedence

**Variable assignment takes precedence over function declaration**

```
var double = 22;
function double(num) {
  return (num*2);
}
console.log(typeof double); // Output: number
```

**Function declarations take precedence over variable declarations.**

```
var double;
function double(num) {
  return (num*2);
} 
console.log(typeof double); // Output: function
```

Function declarations are hoisted over variable declarations but not over variable assignments.

**Hoisting Classes**

Javascript classes are functions, therefore, class declarations are hoisted. However, they remain uninitialised until evaluation. This effectively means that you have to declare a class before you can use it.

### Hoisting and Scope

Each function provides it’s own hoisting scope.  Var declarations are hoisted to the top of the function scope, var assignments are not. Variables declared in functions are limited to that function scope, and are not available outside of that scope

Example

```
function testHoist() {
  console.log(message);
  var message='Hoisting is all the rage!'
}
testHoist();
 
testHoist(); // Ouput: undefined
```


**Hoisting Best Practices** 
Declare all variables,functions, classes  at the beginning of every scope. 


