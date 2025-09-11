# [Chapter 06] Type Conversion and Short-Circuit Evaluation

## 6.1 What is Type Conversion?
> When a developer **intentionally converts the type of a value**, it is called **explicit type conversion** or **type casting**. 

```jsx
let x = 10;

// Explicit type conversion
// Casts the number to a string
let str = x.toString();
console.log(typeof str, str); // string 10

// The value of x itself is not changed
console.log(typeof x, x); // number 10
```

<br>

> **Implicit type conversion (type coercion)** happens when the JavaScript engine automatically converts a value to another type during expression evaluation, regardless of developer intent.

```jsx
let x = 10;

// Implicit type conversion
// String concatenation creates a new string from number x
let str = x + '';
console.log(typeof str, str); // string 10    

// The value of x itself is not changed
console.log(typeof x, x); // number 10
```

👉 Explicit conversion makes the developer’s intent clear in the code.  
However, implicit conversion can sometimes be more readable.  
<br>

Example: explicit: `(10).toString()` / implicit: `10 + ' '`

## 6.2 Implicit Type Conversion

### 6.2.1 Conversion to String
> The engine coerces non-string operands into strings when evaluating string concatenation expressions.

```jsx
`1 + 1 = ${1 + 1}` // -> "1 + 1 = 2" (template literal with expression interpolation)

// Number type
0 + ''         // -> "0"
-0 + ''        // -> "0"
1 + ''         // -> "1"
-1 + ''        // -> "-1"
NaN + ''       // -> "NaN"
Infinity + ''  // -> "Infinity"
-Infinity + '' // -> "-Infinity"

// Boolean type
true + ''  // -> "true"
false + '' // -> "false"

// null type
null + '' // -> "null"

// undefined type
undefined + '' // -> "undefined"

// symbol type
(Symbol()) + '' // -> TypeError: Cannot convert a Symbol value to a string

// object type
({}) + ''           // -> "[object Object]"
Math + ''           // -> "[object Math]"
```
<br>

### 6.2.2 Conversion to Number
> The engine coerces non-number operands into numbers when evaluating arithmetic operations.

```jsx
1 - "1"; // 0

1 * "10"; // 10

1 / "one"; // NaN

"1" > 0; // true
```

```jsx
+""        // 0
+"0"       // 0
+"1"       // 1
+"string"  // NaN
+true      // 1
+false     // 0
+null      // 0
+undefined // NaN
+[]        // 0
+{}        // NaN
+[1, 2]    // NaN
+function(){} // NaN
```
<br>

### 6.2.3 Conversion to Boolean
> The engine implicitly converts values to boolean when evaluating conditions.

```jsx
if ("") console.log("1"); 
if (true) console.log("2"); // "2"
if (0) console.log("3"); 
if ("str") console.log("4"); // "4"
if (null) console.log("5");
// Only the truthy ones run
```
<br>

👉 Values are classified as truthy (evaluated as true) or falsy (evaluated as false).  

- Falsy: false, 0, "", null, undefined, NaN
- Truthy: everything else

## 6.3 Explicit Type Conversion
> Achieved using constructor functions (`String`, `Number`, `Boolean` without `new`), built-in methods, or even by leveraging implicit conversions.

### 6.3.1 Conversion to String
1. `String()` constructor without `new`  
2. `Object.prototype.toString` method  
3. String concatenation with `+`

```jsx
String(1); // "1"
String(NaN); // "NaN"
String(true); // "true"
(1).toString(); // "1"
[1, 2, 3].join(","); // "1,2,3"
1 + "2"; // "12"
```

### 6.3.2 Conversion to Number
1. `Number()` constructor without `new`  
2. `parseInt`, `parseFloat` for strings  
3. Unary `+` operator  
4. Arithmetic with numbers  

```jsx
Number("1"); // 1
Number(true); // 1
Number(false); // 0

parseInt("1"); // 1
parseFloat("5.6"); // 5.6

+"2"; // 2
+true; // 1

1 * "1"; // 1
```

### 6.3.3 Conversion to Boolean
1. `Boolean()` constructor without `new`  
2. Double NOT `!!` (applies negation twice)

```jsx
Boolean("x"); // true
Boolean("false"); // true (non-empty string is truthy)

Boolean(""); // false

Boolean(undefined); // false
Boolean(null); // false

Boolean({}); // true
Boolean([]); // true

!!"x"; // true
!!1; // true

!!undefined; // false
!!null; // false

!!{}; // true
!![]; // true
```

## 6.4 Short-Circuit Evaluation
> Logical OR (`||`) and AND (`&&`) operators may return **non-boolean** values.  
They return one of the operands directly, not always a boolean.

```jsx
// Example 1
"Dog" && "Cat"; // "Cat"
"Dog" || "Cat"; // "Dog"

// Example 2
let loggedIn = true;
let username = 'User1';
loggedIn && console.log('Welcome! ' + username); // "Welcome! User1"

loggedIn = false;
loggedIn && console.log('Welcome! ' + username); // nothing printed
```

👉 Short-circuiting means evaluation stops once the result is determined, returning the operand without conversion.

| Expression          | Result     |
| ------------------- | ---------- |
| true \|\| anything  | true       |
| false \|\| anything | anything   |
| true && anything    | anything   |
| false && anything   | false      |

```jsx
let done = false;
let msg = "";

// if condition
if (done) msg = "Done";

// using &&
msg = done && "Done";
console.log(msg); // Done

let done = false;
let msg = "";

// if condition
if (!done) msg = "Not done";

// using ||
msg = done || "Not done"; 
console.log(msg); // Not done

// if...else
let done = true;
let msg = "";

if (done) msg = "Done";
else msg = "Not done";
console.log(msg); // Done

// Ternary
msg = done ? "Done" : "Not done";
console.log(msg); // Done
```

### 6.4.1 Optional Chaining Operator
> The `?.` operator returns `undefined` if the left-hand operand is `null` or `undefined`, otherwise it accesses the property on the right-hand side.

```jsx
// Example 1
let elem = null;

var value = elem?.value; 
console.log(value); // undefined

let str = "";
let length = str?.length;
console.log(length); // 0

// Example 2
const user = {
    profile: {
        name: "User1",
        details: {
            age: 30,
            location: "Gangnam-gu, Seoul"
        }
    }
};

console.log(user.profile.details.age);  // 30
console.log(user2.profile?.details?.age);  // undefined
```

### 6.4.2 Nullish Coalescing Operator
> The `??` operator returns the right-hand operand if the left-hand operand is `null` or `undefined`, otherwise it returns the left-hand operand.

```jsx
// Example 1
let foo = null || "default string";
console.log(foo); // "default string"

foo = "" || "default string";
console.log(foo); // "default string"

foo = "" ?? "default string";
console.log(foo); // ""
```

```jsx
// Example 2
let userLocation = null;
console.log(userLocation ?? 'Unknown location');  // "Unknown location"

userLocation = 'Seoul';
console.log(userLocation ?? 'Unknown location');  // "Seoul"

const temperature = 0;
console.log(temperature ?? 25);  // 0
```

❗ Difference between Nullish Coalescing (`??`) and Logical OR (`||`):

```jsx
// Logical OR
const display = (item) => {
  const textLength = item.textLength || 50;
  console.log(textLength); // 50 -> because 0 is falsy
  // Nullish Coalescing
  const itemsPerPage = item.itemsPerPage ?? 10;
  console.log(itemsPerPage); // 0 -> because 0 is not null/undefined
};

const userItem = {
  textLength: 0,
  itemsPerPage: 0,
}
```