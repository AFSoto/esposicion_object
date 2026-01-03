# JavaScript Objects - Complete Guide for Class

## Table of Contents
1. [What is an object?](#what-is-an-object)
2. [Syntax and Creating Objects](#syntax-and-creating-objects)
3. [Accessing and Modifying Properties](#accessing-and-modifying-properties)
4. [Methods in Objects](#methods-in-objects)
5. [Nested Objects](#nested-objects)
6. [Arrays of Objects](#arrays-of-objects)
7. [Important Object Methods](#important-object-methods)
8. [Destructuring](#destructuring)
9. [Spread Operator](#spread-operator)
10. [Advanced Concepts](#advanced-concepts)

---

## What is an object?

An **object** in JavaScript is a collection of related properties that represent an entity. It's like a container that groups information and functionality together.

### Without objects (problematic):
```javascript
let personName = "Carlos";
let personAge = 28;
let personProfession = "Developer";
```

### With objects (organized):
```javascript
let person = {
  name: "Carlos",
  age: 28,
  profession: "Developer"
};
```

**Key concept**: An object is a collection of key-value pairs where each property has a name (key) and an associated value.

---

## Syntax and Creating Objects

### 1. Literal Notation (most common)
```javascript
let product = {
  name: "Laptop",
  price: 1500,
  available: true
};
```

### 2. Object Constructor
```javascript
let product = new Object();
product.name = "Laptop";
product.price = 1500;
product.available = true;
```

### 3. Object.create()
```javascript
let product = Object.create(null);
product.name = "Laptop";
product.price = 1500;
```

---

## Accessing and Modifying Properties

### Dot Notation
```javascript
// Access
console.log(person.name); // "Carlos"

// Modify
person.age = 29;

// Add new property
person.city = "New York";
```

### Bracket Notation
```javascript
// Access with variable
let property = "name";
console.log(person[property]); // "Carlos"

// Add property
person["lastName"] = "Gonzalez";

// Property with spaces
let obj = {
  "full name": "Carlos Gonzalez"
};
console.log(obj["full name"]);
```

### When to use brackets?
- When the property name is in a variable
- When the name has spaces or special characters
- To build properties dynamically in loops

---

## Methods in Objects

Objects can have functions as properties, called **methods**.

### Traditional Syntax
```javascript
let calculator = {
  number1: 10,
  number2: 5,
  
  add: function() {
    return this.number1 + this.number2;
  },
  
  subtract: function() {
    return this.number1 - this.number2;
  }
};

console.log(calculator.add()); // 15
```

### Modern Syntax (ES6)
```javascript
let calculator = {
  number1: 10,
  number2: 5,
  
  add() {
    return this.number1 + this.number2;
  },
  
  subtract() {
    return this.number1 - this.number2;
  }
};
```

### The `this` keyword
`this` refers to the current object. It's like saying "this object I'm in".
```javascript
let person = {
  name: "Ana",
  age: 25,
  
  greet() {
    return `Hello, I'm ${this.name} and I'm ${this.age} years old`;
  }
};

console.log(person.greet());
// "Hello, I'm Ana and I'm 25 years old"
```

---

## Nested Objects

Objects can contain other objects as properties.
```javascript
let student = {
  name: "Ana",
  age: 20,
  address: {
    street: "7th Ave",
    number: 123,
    city: "New York",
    country: "USA"
  },
  grades: {
    math: 4.5,
    programming: 5.0,
    english: 4.2
  }
};

// Access nested properties
console.log(student.address.city); // "New York"
console.log(student.grades.programming); // 5.0

// Modify nested properties
student.address.city = "Boston";
```

---

## Arrays of Objects

A very common structure in real applications.
```javascript
let students = [
  { name: "Ana", age: 20, average: 4.2 },
  { name: "Luis", age: 22, average: 3.8 },
  { name: "Maria", age: 21, average: 4.7 },
  { name: "Peter", age: 19, average: 4.0 }
];

// Access a specific student
console.log(students[0].name); // "Ana"

// Iterate with forEach
students.forEach(student => {
  console.log(`${student.name}: ${student.average}`);
});

// Filter students
let outstanding = students.filter(std => std.average > 4.0);

// Map to get only names
let names = students.map(std => std.name);

// Find a student
let ana = students.find(std => std.name === "Ana");
```

---

## Important Object Methods

### Object.keys()
Returns an array with the keys (property names).
```javascript
let person = { name: "Carlos", age: 28, city: "New York" };
let keys = Object.keys(person);
console.log(keys); // ["name", "age", "city"]
```

### Object.values()
Returns an array with the values.
```javascript
let values = Object.values(person);
console.log(values); // ["Carlos", 28, "New York"]
```

### Object.entries()
Returns an array of arrays with [key, value] pairs.
```javascript
let entries = Object.entries(person);
console.log(entries);
// [["name", "Carlos"], ["age", 28], ["city", "New York"]]

// Useful for iteration
Object.entries(person).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

### Object.assign()
Copies properties from one or more objects to a target object.
```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let obj3 = { e: 5 };

let combined = Object.assign({}, obj1, obj2, obj3);
console.log(combined); // { a: 1, b: 2, c: 3, d: 4, e: 5 }
```

### Object.freeze()
Freezes an object, preventing modifications.
```javascript
let config = { apiUrl: "https://api.example.com" };
Object.freeze(config);

config.apiUrl = "another-url"; // No effect
console.log(config.apiUrl); // "https://api.example.com"
```

### Object.seal()
Seals an object: you can modify existing properties but not add/delete.
```javascript
let person = { name: "Carlos", age: 28 };
Object.seal(person);

person.age = 29; // Works
person.city = "New York"; // No effect
delete person.name; // No effect
```

---

## Destructuring

Extract properties from objects in an elegant way.

### Basic Destructuring
```javascript
let person = { name: "Carlos", age: 28, city: "New York" };

// Traditional way
let name = person.name;
let age = person.age;

// With destructuring
let { name, age } = person;
console.log(name); // "Carlos"
console.log(age); // 28
```

### Renaming Variables
```javascript
let { name: personName, age: personAge } = person;
console.log(personName); // "Carlos"
```

### Default Values
```javascript
let { name, age, country = "USA" } = person;
console.log(country); // "USA" (if it doesn't exist in the object)
```

### Nested Destructuring
```javascript
let student = {
  name: "Ana",
  address: {
    city: "New York",
    country: "USA"
  }
};

let { name, address: { city } } = student;
console.log(city); // "New York"
```

### In Function Parameters
```javascript
function showPerson({ name, age }) {
  console.log(`${name} is ${age} years old`);
}

showPerson(person); // "Carlos is 28 years old"
```

---

## Spread Operator

The spread operator (...) allows you to expand objects.

### Copy Objects
```javascript
let person = { name: "Carlos", age: 28 };
let copy = { ...person };

// Modifying the copy doesn't affect the original
copy.age = 30;
console.log(person.age); // 28
```

### Combine Objects
```javascript
let info1 = { name: "Carlos", age: 28 };
let info2 = { city: "New York", profession: "Developer" };

let complete = { ...info1, ...info2 };
// { name: "Carlos", age: 28, city: "New York", profession: "Developer" }
```

### Add/Overwrite Properties
```javascript
let person = { name: "Carlos", age: 28 };
let employee = { ...person, position: "Developer", age: 29 };
// { name: "Carlos", age: 29, position: "Developer" }
// The age is overwritten
```

---

## Advanced Concepts

### Comparing Objects
Objects are compared by reference, not by content.
```javascript
let obj1 = { a: 1 };
let obj2 = { a: 1 };
let obj3 = obj1;

console.log(obj1 === obj2); // false (different references)
console.log(obj1 === obj3); // true (same reference)

// To compare content, use JSON.stringify
console.log(JSON.stringify(obj1) === JSON.stringify(obj2)); // true
```

### Deleting Properties
```javascript
let person = { name: "Carlos", age: 28, city: "New York" };
delete person.age;
console.log(person); // { name: "Carlos", city: "New York" }
```

### Check if a Property Exists
```javascript
let person = { name: "Carlos", age: 28 };

// in operator
console.log("name" in person); // true
console.log("lastName" in person); // false

// hasOwnProperty
console.log(person.hasOwnProperty("name")); // true
```

### Optional Chaining (?.)
Avoid errors when accessing properties that might not exist.
```javascript
let person = {
  name: "Carlos",
  address: {
    city: "New York"
  }
};

// Without optional chaining (might throw error)
// console.log(person.job.company); // Error!

// With optional chaining
console.log(person.job?.company); // undefined (no error)
console.log(person.address?.city); // "New York"
```

### Getters and Setters
```javascript
let person = {
  name: "Carlos",
  lastName: "Gonzalez",
  
  get fullName() {
    return `${this.name} ${this.lastName}`;
  },
  
  set fullName(value) {
    [this.name, this.lastName] = value.split(" ");
  }
};

console.log(person.fullName); // "Carlos Gonzalez"
person.fullName = "Ana Martinez";
console.log(person.name); // "Ana"
```

---

## Class Structure (1 hour)

### Phase 1: Introduction (10 min)
- What are objects and why are they important?
- Real-world examples
- Basic syntax

### Phase 2: Fundamentals (15 min)
- Creating objects
- Accessing and modifying properties
- Dot notation vs brackets

### Phase 3: Advanced Features (15 min)
- Methods and `this`
- Nested objects
- Arrays of objects

### Phase 4: Modern Tools (10 min)
- Object methods
- Destructuring
- Spread operator

### Phase 5: Practical Exercises (10 min)
- Present the 3 exercises
- Answer questions

---

## Practical Exercises

### Exercise 1: Library System (Basic)

Create a `book` object with the following properties:
- title
- author
- year of publication
- number of pages
- available (boolean)

Then add a `description()` method that returns a string with all the book information in a readable format.

**Example output:**
```
"The book 'One Hundred Years of Solitude' by Gabriel Garcia Marquez, published in 1967, 
has 417 pages and is available."
```

---

### Exercise 2: Shopping Cart (Intermediate)

Create a `shoppingCart` object that contains:

**Properties:**
- `products`: array of objects, where each product has name, price, and quantity

**Methods:**
- `addProduct(name, price, quantity)`: adds a product to the cart
- `calculateTotal()`: returns the total price (price × quantity of all products)
- `applyDiscount(percentage)`: applies a discount to the total and returns the new total
- `showProducts()`: displays all cart products in the console

**Usage example:**
```javascript
shoppingCart.addProduct("Laptop", 1500, 1);
shoppingCart.addProduct("Mouse", 25, 2);
console.log(shoppingCart.calculateTotal()); // 1550
console.log(shoppingCart.applyDiscount(10)); // 1395 (10% discount)
```

---

### Exercise 3: Student System (Advanced)

Create an array called `students` where each student is an object with:
- name
- age
- grades (object with subjects and scores)

**Implement the following functions:**

1. `calculateAverage(student)`: returns the average of a student's grades

2. `getBestStudent(students)`: returns the student with the best average

3. `outstandingStudents(students)`: returns an array with students of legal age (≥18) who have an average above 4.0

4. `addGrade(student, subject, grade)`: adds a new grade to the student

**Structure example:**
```javascript
let students = [
  {
    name: "Ana",
    age: 20,
    grades: {
      math: 4.5,
      programming: 5.0,
      english: 4.2
    }
  },
  // ... more students
];
```

---

## Frequently Asked Questions

### What's the difference between objects and arrays?
- **Arrays**: ordered collections, accessed by numeric index
- **Objects**: collections of key-value pairs, accessed by property name

### What happens if I try to access a property that doesn't exist?
Returns `undefined`, doesn't generate an error.

### Can I have functions inside objects?
Yes, they're called methods and are very common.

### Are objects mutable?
Yes, you can modify their properties even if they're declared with `const`. The `const` only prevents reassigning the variable, not modifying the object's content.

### How do I copy an object without modifying the original?
Use spread operator or `Object.assign()` for shallow copies. For deep copies, use `structuredClone()` or JSON parse/stringify.

---

## Additional Resources

- [MDN Web Docs - Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- [JavaScript.info - Objects](https://javascript.info/object)
- Practice at: [Exercism](https://exercism.org/tracks/javascript), [Codewars](https://www.codewars.com/)

---

**Good luck with your class! 🚀**
