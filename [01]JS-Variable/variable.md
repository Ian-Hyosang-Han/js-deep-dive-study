# [Chapter 01] Variables

## 1.1 What is a variable?

A variable is a core concept in programming languages for managing data. A variable refers to the memory space secured to store a single value, or the name attached to that memory space to identify it. Put simply, it is a **symbolic name that points to the location of a value.**

- Variable name: a unique name that can identify the value stored in memory
- Variable value: the value stored in the variable
- Assignment (assignment): storing a value in a variable
- Reference (reference): reading the value stored in a variable

<br>

## 1.2 Identifier

```
What is an identifier? A unique name that can distinguish and identify a value
```

- An identifier remembers a **memory address**, not a value.
- Identifiers are not limited to variable names. Any name that can identify some value existing in memory is also called an identifier.
- An identifier’s existence is made known to the JavaScript engine through **declaration**.

<br>

## 1.3 Variable declaration

What is variable declaration? It means creating a variable, securing memory space, and **linking the variable name with the address of the secured memory space** so it is ready to store a value.

- To use a variable, a declaration is required. When declaring a variable, use the **var, let , const** keywords.

## 1.4 Execution timing of variable declarations and variable hoisting

JavaScript code is executed sequentially, line by line, by the interpreter.

💡 Execution timing of variable declarations: variable declarations are executed **before runtime**, i.e., prior to the phase where the source code is executed sequentially line by line.

❗ Variable hoisting (hoisting): The JavaScript-specific feature where **variable declarations behave as if they are lifted to the top of the code** is called variable hoisting.

```jsx
/* When the variable reference appears before the variable declaration */
console.log(score); // undefined

var score;
```

## 1.5 Value assignment

What is value assignment? When assigning a value to a variable, use the = operator; the assignment operator assigns the value on the right-hand side to the variable on the left-hand side.

```jsx
var score; // variable declaration and value assignment

score = 90; // reassignment

var score = 90; // variable declaration and value assignment
```
- Variable declarations are executed before runtime, but value assignment is executed at runtime, when the source code runs sequentially.

## 1.6 Value reassignment

What is value reassignment? It means assigning a new value again to a variable that already has a value assigned.

```jsx
var score = 80; // variable declaration and value assignment

score = 90; // reassignment
```

- Constant (constant): a variable that cannot be reassigned, so the stored value cannot be changed

=> Since the const keyword forbids reassignment, it can be assigned only once as a constant.

> Garbage Collector: periodically scans memory and releases memory that is no longer used because it is not referenced by any identifier. JavaScript is a managed language with a built-in garbage collector, which prevents memory leaks through the garbage collector.

> Managed language / Unmanaged language <br> 1. Managed Language: Like the C language, it provides low-level memory control functions such as malloc() and free() so that the developer can explicitly allocate and free memory. Because the developer leads and controls memory, a high level of optimization is possible, but the risk of errors is higher. <br><br> 2. Unmanaged Language: JavaScript falls into this category, where the language itself is responsible for memory management functions for allocation and deallocation, and it does not allow the developer’s direct memory control. The garbage collector frees memory that is no longer used. It can secure a certain level of consistent productivity, so it is stable, but some performance loss must be tolerated.

## 1.7 Identifier naming rules

- May include letters, digits, underscores (_), and the dollar sign ($) except for other special characters
- Must start with a letter, underscore (_), or dollar sign ($); starting with a digit is not allowed
- Reserved words cannot be used

### Naming Convention ###

- Naming rules defined to make identifiers composed of one or more English words more readable

```jsx
// camelCase: mainly variables, function names
var firstName;

// PascalCase: mainly constructor functions, class names
var FirstName;

// snake_case
var first_name;

// Hungarian notation (typeHungarianCase)
var strFirstName; // type + identifier
var $elem = document.getElementById("myId"); // DOM node
var observable$ = fromEvent(document, "click"); // RxJS observable
```