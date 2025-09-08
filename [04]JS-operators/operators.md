# [Chapter 04] Operators
> What is an operator? **It performs arithmetic, assignment, comparison, logical, type, exponentiation, and other operations on one or more expressions to produce a single value.**  
> An operator expression—made by combining operands and operators—is also an expression that can be evaluated to a value.

📄 Operand: the target of an operation; an expression that can be evaluated to a value

## 4.1 Arithmetic Operators
> If an arithmetic operation is not possible, it returns `NaN`. Depending on the number of operands, operators are classified as binary arithmetic operators and unary arithmetic operators.

- Binary arithmetic operators: They have no side effects that change the value of the operands. They always produce a new value.

| Binary Arithmetic Operator | Meaning        | Side Effect |
| :------------------------: | :------------: | :---------: |
|             +              | Addition       |      X      |
|             -              | Subtraction    |      X      |
|             \*             | Multiplication |      X      |
|             /              | Division       |      X      |
|             %              | Remainder      |      X      |

```jsx
5 + 2; // 7
5 - 2; // 3
5 * 2; // 10
5 / 2; // 2.5
5 % 2; // 1
```
<br>

- Unary arithmetic operators: Operate on one operand to produce a numeric value.  
❗ The increment/decrement operators `++/--` have side effects because they change the operand’s value.

| Unary Arithmetic Operator |                Meaning                 | Side Effect |
| :-----------------------: | :------------------------------------: | :---------: |
|            ++             |               Increment                |      O      |
|            --             |                Decrement               |      O      |
|             +             | No effect; does **not** flip sign      |      X      |
|             -             | Returns the negated value (flips sign) |      X      |

<br>

❗ Pre-increment/decrement changes the value **before** evaluation; post-increment/decrement evaluates first and **then** changes the value.

```jsx
let x = 5, result;

// assign first, then increment (post-increment)
result = x++;
cossole.log(result, x); // 5, 6

// increment first, then assign (pre-increment)
result = ++x;
cossole.log(result, x); // 7, 7

// assign first, then decrement (post-decrement)
result = x--;
cossole.log(result, x); // 7, 6

// decrement first, then assign (pre-decrement)
result = --x;
cossole.log(result, x); // 5, 5
```

- String concatenation operator:  
  - If **one or more operands are strings**, the operator acts as a string concatenation operator.  
  - Cases 2, 3, 4 below are examples of implicit type conversion (type coercion).

```jsx
// 1. String concatenation
'1' + 2; // '12'
1 + '2'; // '12'

// 2. true is converted to 1
1 + true; // 2

// 3. false is converted to 0
1 + false; // 1

// 4. null is converted to 0
1 + null; // 1

// undefined cannot be converted to a number
+undefined; // NaN
1 + undefined; // NaN
```
<br>

## 4.2 Assignment Operators
> Assigns the evaluation result of the right-hand operand to the variable on the left-hand side.

| Assignment Operator |   Example   | Equivalent Expression | Side Effect |
| :-----------------: | :---------: | :-------------------: | :---------: |
|          =          |   x = 5     |        x = 5          |      O      |
|         +=          |   x += 5    |       x = x + 5       |      O      |
|         -=          |   x -= 5    |       x = x - 5       |      O      |
|         \*=         |   x \*= 5   |       x = x * 5       |      O      |
|         /=          |   x /= 5    |       x = x / 5       |      O      |
|         %=          |   x %= 5    |       x = x % 5       |      O      |

```jsx
var x;

x = 10;
console.log(x); // 10

x += 5;
console.log(x); // 15

x -= 5;
console.log(x); // 10

x *= 5;
console.log(x); // 50

x /= 5;
console.log(x); // 10

x %= 5;
console.log(x); // 0

// String concatenation with assignment
let str = "My name is ";
str += "Lee"; // str = str + 'Lee'
console.log(str); // 'My name is Lee'
```
- An assignment statement is an expression statement; it evaluates to the assigned value.

<br>

## 4.3 Comparison Operators
> **Compare the left and right operands** and return the **result as a boolean value.**  
> Mostly used in conditional statements such as `if` or `for`.

| Comparison Operator | Meaning        | Example  | Description                            | Side Effect |
| :-----------------: | :------------: | :------: | :------------------------------------: | :---------: |
|         ==          | Loose equality | x == y   | True if x and y are equal in value     |      X      |
|        ===          | Strict equality| x === y  | True if x and y are equal in value and type | X   |
|         !=          | Loose inequality | x != y | True if x and y are not equal in value |      X      |
|        !==          | Strict inequality | x !== y | True if x and y are not equal in value or type | X |

```jsx
5 == '5'; // true
5 === '5'; // false
5 != '5'; // false
5 !== '5'; // true
```

```jsx
false == '0'; // true
0 == ''; // true
0 == '0'; // true
false == 'false'; // false
false == null; // false
false == undefined; // false
```

❗ Loose equality (`==`) produces unpredictable results. Avoid using it and use strict equality (`===`) instead.

```jsx
// Beware of NaN and 0
NaN === NaN; // false -> NaN is the only value not equal to itself
Number.isNaN(NaN); // true -> use Number.isNaN to check

// Positive and negative zero comparisons return true
0 === -0; // true
0 == -0; // true

// Object.is provides predictable comparison results
-0 === +0; // true
Object.is(-0, +0); // false 

NaN === NaN; // false
Object.is(NaN, NaN); // true
```
<br>

## 4.4 Ternary Conditional Operator
> Determines the return value based on the evaluation result of the condition. No side effects.

```jsx
let x = 2;

// 2 % 2 is 0, and 0 is coerced to false
let result = x % 2 ? "Odd" : "Even";
console.log(result); // Even
```

❗ Difference between ternary operator and `if...else`:  
The ternary operator expression can be used as a value, whereas `if...else` cannot.

<br>

## 4.5 Logical Operators
> Performs logical operations on the left and right operands.

| Logical Operator | Meaning       | Side Effect |
| :--------------: | :-----------: | :---------: |
|        \|\|      | Logical OR    |      X      |
|        &&        | Logical AND   |      X      |
|        !         | Logical NOT   |      X      |

```jsx
// Logical OR (||) -> true wins!
true || true; // true
true || false; // true
false || true; // true
false || false; // false

// Logical AND (&&)
true && true; // true
true && false; // false
false && true; // false
false && false; // false

// Logical NOT (!)
!true; // false
!false; // true
!0; // true  -> implicit coercion
!"hello"; // false -> non-empty strings are truthy

// Short-circuit evaluation
"Cat" && "Dog"; // Dog
```
<br>

## 4.6 Comma Operator
> Evaluates operands from left to right, and returns the result of the last operand.

```jsx
var x, y, z;
(x = 1), (y = 2), (z = 3); // 3
```
<br>

## 4.7 Grouping Operator
> Parentheses group expressions and force them to be evaluated first. The grouping operator has the highest precedence.

```jsx
10 * 2 + 3; // 23

// Adjust precedence using grouping
10 * (2 + 3); // 50
```
<br>

## 4.8 `typeof` Operator
> The `typeof` operator returns the type of its operand as a string.

```jsx
typeof " "; // string
typeof 1; // number
typeof NaN; // number
typeof true; // boolean
typeof undefined; // undefined
typeof Symbol(); // symbol
typeof []; // object
typeof {}; // object
typeof new Date(); // object
typeof /test/gi; // object
typeof function () {}; // function

// null
typeof null; // object   -> bug

var foo = null;
typeof foo === null; // false -> typeof foo returns "object"
foo === null; // true
```
<br>

## 4.9 Exponentiation Operator
> Raises the left operand to the power of the right operand and returns the result.

```jsx
2 ** 2; // 4
2 ** 0; // 1

Math.pow(2, 2); // 4
Math.pow(2, 0); // 1
```
<br>

## 4.10 Other Operators

| Operator   | Description                                                                 |
| :--------: | :-------------------------------------------------------------------------- |
|     ?.     | Optional chaining operator                                                   |
|     ??     | Nullish coalescing operator                                                  |
|   delete   | Deletes a property                                                           |
|    new     | Creates an instance by calling a constructor function                        |
| instanceof | Checks if the left object is an instance created by the right constructor    |
|     in     | Checks for property existence                                                |

<br>

## 4.11 Side Effects of Operators
- Some operators affect other code:
  - Assignment operator (`=`)
  - Increment/decrement operators (`++ / --`)
  - `delete` operator

<br>

## 4.12 Operator Precedence
> The order in which operators are executed when multiple are present in a statement.

| Precedence | Operators                                                                 |
| ---------- | ------------------------------------------------------------------------- |
| 1          | ()                                                                        |
| 2          | new (with args), ., [], (), ?.(optional chaining)                         |
| 3          | new (without args)                                                        |
| 4          | x++, x--                                                                  |
| 5          | !x, +x, -x, ++x, --x, typeof, delete                                      |
| 6          | ** (highest precedence among binary operators)                            |
| 7          | *, /, %                                                                   |
| 8          | +, -                                                                      |
| 9          | <, <=, >, >=, in, instanceof                                              |
| 10         | ==, !=, ===, !==                                                          |
| 11         | ?? (nullish coalescing)                                                   |
| 12         | &&                                                                        |
| 13         | \|\|                                                                      |
| 14         | ? ... : ...                                                               |
| 15         | Assignment (=, +=, -=, ...)                                               |
| 16         | ,                                                                         |

- It’s recommended to use grouping operators to explicitly control precedence.

<br>

## 4.13 Operator Associativity
> Defines whether operators are evaluated from the left or the right.

| Associativity | Operators                                                               |
| :-----------: | :---------------------------------------------------------------------- |
| Left-to-right | +, -, /, %, <, <=, >, >=, &&, [], (), ??, ?., in, instanceof            |
| Right-to-left | ++, --, assignment, !x, +x, -x, ++x, --x, typeof, delete, ? ... : ...   |
