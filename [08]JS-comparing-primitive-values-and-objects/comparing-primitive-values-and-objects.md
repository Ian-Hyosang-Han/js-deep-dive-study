# [Chapter 08] Comparing Primitive Values and Objects

## 8.1 Primitive Values

Data types

- **Primitive type**: immutable value → when you **assign a primitive to a variable**, the **actual value is stored** in the variable.
- **Object type**: reference type (objects are mutable) → when you **assign an object to a variable**, the **reference (address) is stored** in the variable.
  <br>

### 8.1.1 Immutable Values

> A statement about **values**, not variables: primitive values are immutable.

```jsx
const o = {}; // A variable declared with const cannot be reassigned.

// A constant (primitive value) assigned to a const variable cannot be changed,
// **but an object assigned to a const variable can have its contents mutated.**
o.a = 1;
console.log(o); // { a: 1 }
```

<br>

- **What is immutability?** <br>
  **Primitive values cannot be changed in place.** To “change” a primitive a variable holds, you allocate a new memory space, store the new value there, and update the variable to reference the new address.  
  👉 For variables holding immutable primitives, **reassignment** is the only way to “change” the value.

<br>

### 8.1.2 String Type

> JavaScript provides a primitive **string** type. Strings are **immutable**.

```jsx
// 'str' first points to "qkqh", then to "mimi".
// The original string wasn't changed; the reference moved to a new string.
let str = "qkqh";
str = "mimi";
console.log(str); // "mimi"
```

<br>

- **Array-like object**:  
  An object you can access with indices and that has a `length` property. A string behaves like an array for read access and can be iterated (e.g., with a `for` loop).
- With `str = "mimi";`
  👉 Doing `str[0] = 'm'` does **not** change the string.
  **Once created, a string is read-only and cannot be mutated in place — this guarantees reliability.**

<br>

### 8.1.3 Pass-by-Value (for primitives)

> When you assign a variable that holds a primitive (the “original”) to another variable (the “copy”), the **value is copied** into a different memory location.

```jsx
let score = 90;

let copy = score;
console.log(score, copy); // 90 90 (look the same, but stored separately)
console.log(score === copy); // true
```

👉 `score` and `copy` hold **separate** values in **different memory locations**.

- Strictly speaking, variables store **addresses**. Identifiers remember addresses, not the value itself; via that address we access the value.
- In the end, two primitive values are stored independently.
- **Reassigning** one will not affect the other.

<br>

## 8.2 Objects

> Objects can have a variable number of properties and can be modified by adding/removing properties dynamically.

<br>

### 8.2.1 Mutable Values

> Objects (reference types) are **mutable**.

```jsx
let person = {
  name: "Lee",
};

person.name = "Han";
person.address = "Seoul";
console.log(person); // { name: "Han", address: "Seoul" }
```

<br>

👉 Unlike primitives, **multiple identifiers can reference the same object**.  
Objects are designed as mutable to use memory efficiently.

- **Shallow copy vs. deep copy** <br>
  A **shallow copy** copies only one level; nested objects are **shared**.  
  A **deep copy** recursively copies all nested objects.

```jsx
let p = { x: { y: 1 } };

// Shallow copy
const c1 = { ...p };
console.log(c1 === p); // false
console.log(c1.x === p.x); // true (nested object is shared)

// Deep copy (example using lodash's cloneDeep)
const c2 = _.cloneDeep(p);
console.log(c2 === p); // false
console.log(c2.x === p.x); // false
```

<br>

### 8.2.2 Pass-by-Reference (what people call it)

> Commonly described as “pass-by-reference,” but in JavaScript what’s actually copied is the **reference value** itself.

- Both “pass-by-value” (primitives) and the so-called “pass-by-reference” (objects) **copy what the identifier stores**.
- In JavaScript, there is **only pass-by-value**:
  - For primitives, the value itself is copied.
  - For objects, the **reference (address)** is copied.

```jsx
let person = {
  name: "Lee",
};

let copy = person;

// 'copy' and 'person' reference the same object
console.log(copy === person); // true

// Change via 'copy'
copy.name = "Han";

// Change via 'person'
person.address = "Seoul";

// Mutations through either variable affect the same underlying object
console.log(person); // { name: "Han", address: "Seoul" }
```
