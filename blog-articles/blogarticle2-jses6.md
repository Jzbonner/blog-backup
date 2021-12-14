[comment]: # (Brainstorming ideas for blog articles) 
[comment]: # (Images will not be rendered in Markdown this is just to give reference to the proposed image) 

# JavaScript - ES6 Syntax and Core Functionality
## Part 1: Var, Let, Const and the Importance of Scope
Variable scoping is not a new feature to JavaScript, the use of `var` allowed for variables to be declared in a global manner; but there was nothing built into JavaScript that provided proper lexical scoping. *Lexical scoping* is a convention that sets the scope or range of functionality of a variable so that it may only be referenced from within the block of code in which it is defined. A **variable** by definition is a named space in the memory that stores values. Variable names are called *identifiers* and have a set of naming conventions that must be followed: 
  1. Identifiers can't be keywords 
  2. Identifiers can contain alphabets and numbers 
  3. Identifiers cannot contain spaces and special characters (except for`_` and `$`)
  4. Variable names cannot being with a number 

When working with variables you have to initialize them via declaration. As of ES6 there are 3 main ways declare a variable; Using `var`, `let`, & `const`. 

```javascript
//Syntax for declaring a Variable using the var keyword
var variable_name = variable_value

//Example variable declaration 
var name = "Leon"
console.log("The value in the variable is:" + name)

//Output 
`The value in the variable is Leon`
```

JavaScript (excluding TypeScript) is an un-typed language, meaning that JavaScript variables can point to a value of any data type. The value type of a variable can change during the execution of a program and JavaScript will assign a type dynamically; this is know as **dynamic typing**. This dynamic paradigm in JavaScript isn't so easily applied when considering *scope*. Initially JavaScript only defined two scopes: 
  1. **Global Scope**: These variables can be accessed from within any part of the JavaScript code  
  2. **Local Scope**: These variables can be accessed with a declared function in the JavaScript code

```javascript
/*an example function that shows how a global variable can have its value accessed and manipulated from within all parts of the code.*/
var carsProduced  = 10 
var initialResult = `the initial amount of Cars Produced: ${carsProduced}` 
console.log(initialResult) // => carsProduced amount is 10

function carsMade(amountProduced) {
  carsProduced += amountProduced 
  var updatedResult = `the new amount of Cars Produced: ${carsProduced}.` 
  console.log(updatedResult) // => carsProduced amount is 20
}

/*calling the carsMade function with a parameter of 10*/
carsMade(10) 
```

The above example illustrates how the variable `carsProduced` is initialized and declared outside the `carsMade` function. Since `carsProduced` is a global variable you can  access it in the `carsMade` function and update the total number of `carsProduced` by the `amountProduced` parameter - in this case its 10.


```javascript
/*an example function that shows how a variables can be scoped locally to restrict their range of use to a particular part of the code; in this case the carsMade function.*/
var carsProduced  = 10 
var initialResult = `the initial amount of Cars Produced: ${carsProduced}`   
console.log(initialResult) // => carsProduced amount is 10

function carsMade(amountProduced) {
  var carsProduced = 40 // locally scoped variable
  carsProduced += amountProduced // carsProduced in this statement is referring to the locally scoped variable 
  var updatedResult = `the new amount of Cars Produced: ${carsProduced}.` 
  console.log(updatedResult) // => carsProduced amount is 50
}

/*calling the carsMade function with a parameter of 10*/
carsMade(10) 
```

The above illustrates how the variable `carsProduced` is being declared in the local scope of the `carsMade` function, and then updated with the addition of the value of the `amountProduced` parameter. 

Beyond global and local scope, JavaScript also allows the use of block scope to work with variables in a specified code block only. The `var` variable keyword ignores code blocks; meaning all `var` initialized variables are either function scoped or global scoped (if defined within a code block and not globally they are then hoisted to the top as an implied `undefined` variable). In order to restrict a variables access to a particular code block you have to use the `let` or `const` keyword. 

The benefits of using the `let` keyword ensure that you can refine variable usage to the specific code blocks that require access and limit the amount of accessible variables to the public API. If you attempt to declare a `let` variable twice within the same block, it will throw an error; but it is acceptable to declare a `let` variable in different block level scopes without syntax errors. 

```javascript 
let count = 0 
for (let i = 0; i <=5; i++) {
  count++
  console.log(`this is the value of the block scoped variable: ${count}`)
}

/*this will not throw a ReferenceError since it is declared within the global 
  scope*/
console.log(count)

/*this will throw a RefernenceError since it is declared with the `let` 
  keyword within the for loop and attempting to be referenced outside of 
  that code block */
console.log(i) 
```

The `const` declaration creates a read-only reference to a value. It does not mean the value it holds is immutable, just that the variable identifier cannot be reassigned. Constants are block-scoped, much like variables defined using the `let` keyword. 
  1. Constants cannot be reassigned a value
  2. A constant cannot be re-declared 
  3. A constant requires as intializer (this means constants must be initialized during its declaration)
  4. The value assigned to a constant variable is mutable. 

An example of the immutable properties of `const`: 

```javascript
//declaring and initializing a `const` variable
const CONSTANT_NAME = value 

// `const` variables can't be reassigned a value; and they must be initialized at declaration
const test 
console.log(test) // will return SyntaxError 

const amount = 10
amount = 20 
console.log(amount) // will return TypeError
```

The `const` keyword also has certain restrictions when it's applied to arrays and objects in JavaScript. When an array is designated as a `const` the values of that array can be manipulated but they cannot be reassigned. The same is true for JavaScript objects. 

```JavaScript
/* Declaring an array with the `const` keyword doesn't restrict Array methods from being accessible, but the arrays themselves can not be reassigned*/
const carColors = ['black', 'silver', 'green', 'blue']
carColors.push('red')
console.log(carColors) // will return ['black', 'silver', 'green', 'blue', 'red']

// Array Methods that alter the data of the const declared array are 
carColors.pop() 
carColors.pop()
console.log(carColors) // will return ['black', 'silver']

carColors = [] // will return TypeError  due to reassignment

// Iterating through arrays, maps,and sets with the for...of ES6 syntax, using lets and const 
const classGrades = [88, 92, 85, 96]
for (let score of classGrades) {
  console.log(score) // iterates through the classGrades array and returns every index value 
}

//`const` declared-objects also have similar mutable properties as arrays 
const person = {
  age: 20, 
  name: 'John', 
  job: 'developer'
}

// these assignments will not return an error because the objects property values are mutable
person.age = 30 
person.job = 'data scientist'

console.log(`this is the person's new age: ${person.age}`) // this is the person's new age: 30
console.log(`this is the person's new job: ${person.job}`) // this is the person's new job: data scientist 
```

