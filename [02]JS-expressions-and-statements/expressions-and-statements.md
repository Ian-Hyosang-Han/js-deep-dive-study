# [Chapter 02] Expressions and Statements

## 2.1 Values

> A value is the result produced by evaluation. Here, evaluation means interpreting an expression to produce or reference a value.

- Example

```jsx
// 10 + 20 is evaluated to produce the numeric value 30.
10 + 20;
```

<br />

All values have a data type and are laid out in memory as **binary, i.e., bits**. They **can be interpreted differently depending on the data type**. Values can be created in various ways.  
**e.g.) 0100 0001 → number 65, character 'A'**

<br />
 <br />
 
## 2.2 Literals
 > A literal is a notation that **creates a value using human-readable characters or agreed-upon symbols**.

The JavaScript engine evaluates literals at runtime, when the code is executed, to create values.

- Example

```jsx
// 100 is a literal
var score = 100;
```

 <br />
 <br />
 
## 2.3 Expressions
 > **An expression is something that can be evaluated.** When an expression is evaluated, it either creates a new value or references an existing one.
<br />

A literal is also an expression; a literal by itself is an expression.  
Expressions can be composed of literals, identifiers (names of variables, functions, etc.), operators, and function calls. In other words, **any statement that can be evaluated to a value is an expression.**
<br />

- Example

```jsx
// Literal expressions
10;
("Hello");

// Identifier expressions (assuming the declarations already exist)
sum;
person.name;
arr[i];

// Function/method call expressions (assuming the declarations already exist)
sqare();
person.getName();
```

 <br />

## 2.4 Statements

> A statement is **the basic building block of a program and the smallest unit of execution.**
> <br />

A program is formed by a set of statements, and programming is the act of writing statements and arranging them in order.

<br />

✔ What is a token? It means **the smallest grammatical element of code that cannot be further divided**.<br />
👉 e.g., keywords, identifiers, operators, literals, semicolons (;), special symbols
<br />
<br />

## 2.5 Semicolons and Automatic Semicolon Insertion (ASI)

> A semicolon (;) denotes the end of a statement.
> The JavaScript engine uses semicolons to determine where a statement ends and executes statements sequentially.
> <br />
> But 👉 do not append a semicolon after a code block ({ ... }). Such code blocks are self-terminating and inherently indicate the end of a statement.
> In short, omission is possible, but since the general convention is to recommend semicolons, it’s better to include them.
> <br />
> <br />

## 2.6 Expression Statements vs. Non-Expression Statements

> The simplest and clearest way to distinguish an expression statement from a non-expression statement is to try assigning it to a variable.
> <br />

- Example

```jsx
// A non-expression statement cannot be used like a value.
var foo = var x;

// A variable declaration statement is a non-expression statement.
var x;

// An assignment is itself an expression but also a complete statement. In other words, an assignment is an expression statement.
x = 100;

// An expression statement can be used like a value.
var foo = x = 100;
console.log(foo); // 100
```
