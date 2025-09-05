# [Chapter 03] Data Types

> The required size of memory, the binary stored in memory, and the way it is interpreted all differ depending on the data type.
> Developers create values with a clear intent by distinguishing types,
> and the JavaScript engine handles values by distinguishing their types.

<br>

## 3.1 Number Type

> JavaScript has only one number type.
<br>
👉 In JavaScript, there is no separate type just for integers; all numbers are treated as floating point.

<br>
<br>
- Example

```jsx
// All number values are treated as floating point.
console.log(1 === 1.0); // true

var binary = 0b01000001; // binary
var octal = 0o101; // octal
var hex = 0x41; // hexadecimal

console.log(binary); // 65
console.log(octal); // 65
console.log(hex); // 65
console.log(binary === octal); // true
console.log(octal == hex); // true
```

<br>

The number type can also represent three special values.
<br>
⚠ JavaScript is case-sensitive, so do not write `nan`—use `NaN`.
<br>
<br>
- Example

```jsx
// Three special values of the number type
console.log(10 / 0); // Infinity: positive infinity
console.log(10 / -0); // -Infinity: negative infinity
console.log(1 * "String"); // NaN: arithmetic operation not possible
```

<br>

## 3.2 String Type

> The string type is **used to represent text data.** It is a set of zero or more 16-bit Unicode characters (UTF-16), which can represent most characters.
<br>
⚠ If you do not enclose a string, even whitespace characters like spaces cannot be included.

<br>

```jsx
var string;
string = 'string'; // single quotes
string = "string"; // double quotes
string = `string`; // backticks (ES6)

string = 'Within a string wrapped in single quotes, "double quotes" are recognized as part of the string.';
string = "Within a string wrapped in double quotes, 'single quotes' are recognized as part of the string.";

var string = hello; // hello without quotes is recognized as an identifier (ReferenceError)
```

<br>

## 3.3 Template Literals

> Template literals were introduced in ES6 as a new string notation.

**Template literal features**

- Multi-line strings
- Expression interpolation
- Tagged templates
 <br>
  👉 These features provide convenient string handling, and at runtime they are converted to normal strings for processing.
<br>
<br>

- Example

```jsx
var template = `Template literal`;
console.log(template); // Template literal

// Multi-line strings
var dspText = "";
dspText += "This is an alert box.";
dspText += "\n1.";
dspText += "\n2.";

alert(dspText);

// Output
// This is an alert box.
// 1.
// 2.

var template2 = `<ul>
<li><p>Hi</p><li>
</ul>`;

console.log(template2);

// Output

//<ul>
// <li><p>Hi</p><li>
// </ul>
```

<br>

## 3.4 Boolean Type

> The boolean type represents **logical true or false** with **true** and **false**.

<br>

## 3.5 `undefined` Type

> The only value of the `undefined` type is `undefined`.
<br>
👉 A variable declared with `var` is implicitly initialized to `undefined`. Instead of leaving the allocated memory space empty until the first assignment occurs, it is initialized to `undefined`. If you reference an unassigned variable, `undefined` is returned.
<br>
<br>

- Example

```jsx
var foo;
console.log(foo); // undefined
```

<br>

## 3.6 `null` Type

> The only value of the `null` type is `null`. JavaScript is case-sensitive, so you must write it as `null` when coding.
<br>
👉 Use `null` to explicitly indicate that a variable has no value (intentional absence).
<br>
<br>

- Example

```jsx
var foo = "Lee";

foo = null;
```
<br>

## 3.7 Symbol Type

> A primitive value that is immutable. It is unique. It is mainly used to create property keys.
<br>

```jsx
var key = symbol("key");
console.log(typeof key); // symbol

var obj = {};

// Use a symbol—a unique value with no risk of name collisions—as a property key.
obj[key] = "value";
console.log(obj[key]); // value
```
<br>

## 3.8 Object Type

> JavaScript is an object-based language, and **almost everything that makes up JavaScript is an object**.

 <br>

## 3.9 Why Data Types Are Needed

> When storing and referencing values in memory, you need to determine the size of the memory space, and you need to know whether values can be stored without waste or loss.
 <br>
 👉 In summary:

- To determine the **size of the memory space** to allocate when storing a value
- To determine the **size of the memory space** to read at once when referencing a value
- To determine **how to interpret the binary** read from memory

<br>

## 3.10 Dynamic Typing

> Unlike statically typed languages, JavaScript does not declare a type when declaring variables. **You can freely assign values of any data type.**
<br>
👉 In JavaScript, a variable’s type is determined by its assignment (type inference), and the variable’s type can change dynamically through reassignment.
<br>
<br>

```jsx
foo = {}; // object
console.log(typeof foo); // object

foo = []; // array
console.log(typeof foo); // object

foo = function () {}; // function
console.log(typeof foo); // function
```

<br>

## ⚠ Things to Watch Out for When Using Variables

- Use variables only when necessary and as sparingly as possible. The more variables you have, the higher the chance of errors.
- Make the scope of variables as narrow as possible to minimize side effects.
- Avoid using global variables as much as possible. Because they can be referenced/changed from anywhere, there’s a high chance they will be changed unintentionally and affect other code.
- Prefer constants over variables to prevent changes to values.
- Name variables so that their purpose or meaning is clear. The same applies to identifiers, functions, and class names—choose appropriate names.
