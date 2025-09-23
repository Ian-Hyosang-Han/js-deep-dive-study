# [Chapter 07] Object Literals

## 7.1 What is an Object?
 > Primitive types represent a single immutable value, but object types are **complex data structures that group multiple values of various types into a single unit**. Objects are mutable values.

```javascript
let person = {
   name: 'Lee', // property
   age : 20    // property

// name, age = property keys
// 'Lee', 20 = property values
}

let counter = {
   num : 0, // property
   increase : function (){  // method
    this.num++; 
  }
}
```

## 7.2 Creating Objects with Object Literals

In languages like C++ or Java, a class must be defined first, and then instances are created using a constructor and the `new` operator.

📄 Instance: A concrete entity created by a class and stored in memory.  

- Ways to create objects:
1. Object literal
2. `new Object()` constructor
3. Custom constructor function
4. `Object.create`
5. Class

```javascript
let person = {
  name : 'Lee',
  sayHello : function (){
    console.log(`Hello My name is ${this.name}.`)
  }
};

console.log(typeof person); // object
console.log(person) // {name: "Lee", sayHello: f}
```

## 7.3 Properties
> An object is a collection of properties, and each property is composed of a key and a value.

```javascript
const person = {
  name: 'Lee', 
  // Property key: name (any string including empty strings and symbols) 
  // Property value: 'Lee' (any valid JS value)
};
```

❗ Notes on properties:
- If the name does not follow identifier naming rules, it must be enclosed in quotes.
- It is recommended to follow identifier naming rules for property keys.

```javascript
const person = {
   firstName : 'Ian', // valid key
   'last-name': 'Lee' // invalid identifier -> treated as expression
}

console.log(person); // {firstName : "Ian",  last-name: "Lee" }
```

```javascript
var obj1 = {
  0: 1,
  1: 2,
  2: 3, 
  // Numeric keys are automatically converted to strings internally
};

var obj2 = {
  var: "",
  function: "", // reserved words can be used as keys, but not recommended
};

var obj3 = {
  name : 'Lee',
  name : 'Kim' 
  // No error, but the last one overwrites the first, not recommended
};
```

## 7.4 Methods
> Functions are first-class objects, so they can be used as property values.

```javascript
var circle = {
  radius : 5, // property

  getDiameter : function (){ // method
    return 2 * this.radius // 'this' refers to circle
  }
};

console.log(circle.getDiameter()); // 10
```

## 7.5 Accessing Properties
- Dot notation (`.` operator)
- Bracket notation (`[]` operator)

```javascript
let person = {
   name: 'Lee'
};

// Dot notation
console.log(person.name); // Lee
// Bracket notation
console.log(person['name']); // Lee -> key must be a string in quotes
```

## 7.6 Updating Property Values
> Assigning a new value to an existing property updates the value.

```javascript
var obj2 = {
  name : 'Lee',
};

obj2.name = 'Kim'
console.log(obj2) // {name: "Kim"}
```

## 7.7 Dynamic Property Creation
> Assigning a value to a non-existing property adds the property dynamically.

```javascript
var obj2 = {
  name : 'Lee',
};

obj2.age = 20
console.log(obj2) // {name: "Lee", age : 20}
```

## 7.8 Deleting Properties
> The `delete` operator removes a property from an object.

```javascript
var obj2 = {
  name : 'Lee',
};

obj2.age = 20

delete obj2.age;      // deletes existing property
delete obj2.address;  // no error if property doesn’t exist

console.log(obj2) // {name: "Lee"}
```

## 7.9 ES6 Enhancements to Object Literals

### 7.9.1 Property Shorthand
- When a property value is a variable with the same name as the key, you can use shorthand.

```javascript
let x = 1, y = 2

let obj2 = {
  x: x,
  y: y
};

console.log(obj2) // { x: 1, y: 2 }

let obj3 = { x, y };

console.log(obj3) // { x: 1, y: 2 }
``` 

### 7.9.2 Computed Property Names
- Property keys can be computed dynamically from expressions.

```javascript
let prefix = "prop";
let i = 0;

let obj = {};
obj[prefix + "-" + ++i] = i; // obj["prop-1"] = 1;
obj[prefix + "-" + ++i] = i; // obj["prop-2"] = 2;
obj[prefix + "-" + ++i] = i; // obj["prop-3"] = 3;

console.log(obj) // {prop-1: 1, prop-2: 2, prop-3: 3 }
```

### 7.9.3 Method Shorthand
- Methods can be defined without the `function` keyword.

```javascript
const obj = {
    sayHi() { 
      console.log(`Hi`); 
    }
}
obj.sayHi(); // Hi
```
