# [Chapter 05] Control Flow Statements

> Used to execute a code block conditionally (conditional statements) or repeatedly (loops).

👉 Code normally executes sequentially from top to bottom, but control flow statements allow us to manipulate the flow. <br>
❗ However, changing execution order can make code confusing and error-prone. In functional programming, higher-order functions (`forEach`, `map`, `filter`, `reduce`) are often used to reduce reliance on control flow statements and manage complexity. 

## 5.1 Block Statement
> A block statement (or simply a block) groups zero or more statements enclosed in curly braces.  
- It can be used alone but is generally used with control statements or function definitions.

❗ A block is self-terminating, so do **not** put a semicolon after it.

## 5.2 Conditional Statements
> A conditional statement decides which code block to execute based on the evaluation of a condition.

### 5.2.1 if...else Statement
> The `if` statement executes a code block depending on whether the condition (an expression evaluated to a boolean) is true or false.

```jsx
if (condition1) {
  ...
} else if (condition2) {
  ...
} else {
  ...
}
```

### 5.2.2 switch Statement
> Evaluates an expression and transfers control to the `case` clause with a matching value. <br>

👉 If no `case` matches, control goes to the `default` clause. The `default` clause is optional.

```jsx
let month = 2;
let monthName;

switch (month) {
  case 1: monthName = 'January';
  case 2: monthName = 'February';
  case 3: monthName = 'March';
  default: monthName = 'Invalid month';
}
console.log(monthName); // Prints "Invalid month" instead of "March"
```

👉 This happens because execution continues until the end of the switch statement. This is called **fall through**. <br>
Since there are no `break` statements, `"Invalid month"` is printed.

<br>

```jsx
// Example with break
let month = 2;
let monthName;

switch (month) {
  case 1:
    monthName = "January";
    break;
  case 2:
    monthName = "February";
    break;
  case 3:
    monthName = "March";
    break;
  default:
    monthName = "Invalid month";
}
console.log(monthName); // "February"
```

<br>

## 5.3 Loops

### 5.3.1 for Loop
> Executes a block as long as the condition evaluates to true. Repeats until the condition is false.  
<br>

```jsx
for (let i = 0; i < 2; i++) {
  console.log(i);
}
// 0 1
```

### 5.3.2 while Loop
> Executes a block repeatedly while the condition evaluates to true. Often used when the number of iterations is unknown.

❗ To avoid infinite loops, include an exit condition (often using `if` and `break`) inside the loop.

```jsx
while (count < 3) {
  console.log(count); 
  count++;
  if (count === 3) break; // exit when count reaches 3
}
// 0 1 2
```

### 5.3.3 do...while Loop
> Executes the block first, then evaluates the condition. Ensures the block runs at least once. <br>

```jsx
let count = 0;
do {
  console.log(count);  // 0 1 2
  count++;
} while (count < 3);
```

👉 Other alternatives to loops:
- `forEach` (iterates over arrays)
- `for...in` (enumerates object properties)
- `for...of` (introduced in ES6, iterates over iterables)

<br>

## 5.4 break Statement
> Exits from a labeled statement, a loop, or a `switch` block. <br>
❗ Using `break` outside these contexts causes a `SyntaxError`.

```jsx
if (true) {
  break; // Uncaught SyntaxError: Illegal break statement
}

// Labeled statement
foo: console.log("foo");

// Labeled for loop named "outer"
outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i + j === 3) break outer; // exits the "outer" loop
    console.log(`inner [${i}, ${j}]`);
  }
}
console.log("Done");
```
<br>

❗ Labeled statements are useful for breaking out of nested loops, but they reduce readability and increase error risk, so they are generally discouraged.

<br>

## 5.5 continue Statement
- Skips the current iteration and moves execution to the next iteration of the loop (to the increment step if present). <br>
❗ Unlike `break`, it does not exit the loop.
