JavaScript Interview Questions and Answers
========================================================

1. What are the data types in JavaScript?
JavaScript has eight data types, divided into two categories: primitive and non-primitive (object).

let number = 100;
let string = "hi";
let boolean = true;
let undefinedValue;
let nullValue = null;
let symbol = Symbol("unique");
let bigInt = 123455655555n;
let object = {name: "vijay", age: 21}


2. What is the difference between == and ===?
The == (equality) and === (strict equality) operators are used for comparison in JavaScript.
== (Equality): Performs type coercion before comparison and then it compares values after converting them to a common type.
=== (Strict Equality): Does not perform type coercion and it compares both value and type.

example:
console.log(5 == '5'); //true (compares string to number)
console.log(5==='5'); // false (different types)

3. What is the difference between null and undefined?
Null and undefined are both used to represent the absence of a value.
Null: Must be explicitly assigned. Typeof null returns "object" (this is a known JavaScript bug)
Undefined: Represents a variable that has been declared but not assigned a value .Typeof undefined returns "undefined"

let nullVar = null;
console.log(nullVar); //null
console.log(typeOf null); //"object"

let undefinedVar;
console.log(undefinedVar); //undefined
console.log(typeOf undefined); //"undefined"

4. Explain the concept of hoisting in JavaScript.
Hoisting is a behavior in JavaScript where variable and function declarations are moved to the top of their respective scopes during the compilation phase, before the code is executed. 
This means that regardless of where variables and functions are declared in the code, they are treated as if they are declared at the beginning of their scope.

example:
console.log(x); //output: undefined
var x = 5;
console.log(x); //output: 5

the declaration of x is hoisted to the top, but not its initialization. That's why the first `console.log outputs undefined.

let and const declarations are hoisted but not initialized. This leads to a "temporal dead zone" where accessing the variable before its declaration results in a ReferenceError.

console.log(y);
// throws ReferenceError: Cannot access 'y' before "initialization"
let y = 10;



5. What is the difference between let, const, and var?

var: Function-scoped or globally-scoped. Can be redeclared and updated and Hoisted and initialized with undefined.

let: Block-scoped. Hoisted but not initialized (Temporal Dead Zone).

const: Block-scoped. Cannot be updated or redeclared. Hoisted but not initialized (Temporal Dead Zone)

const a = 10;
a=20; // can't do this


6. What is variable scope in JavaScript?
Variable scope refers to the context in which a variable is declared and can be accessed. In JavaScript, there are two main types of scope:
Global Scope: Variables declared outside any function or block
Local Scope: Variables declared inside a function or block
JavaScript uses lexical scoping, which means that inner functions have access to variables in their outer scope.

let globalVar = "global";

function exampleFuntion(){
    let localVar = "local";

    console.log(globalVar); // "global"
    console.log(localVar); // "local"
}

exampleFuntion();
console.log(globalVar); // global
console.log(localVar);  // ReferenceError: localVar is not defined


7. Explain the difference between global and local variables.
Global Variables: Declared outside any function or block. Accessible from anywhere in the code, including inside functions. Have global scope
Local Variables: Declared inside a function or block. Only accessible within that function or block. Have local scope



8. What is the temporal dead zone?
The Temporal Dead Zone (TDZ) is the period between entering a scope and the point where a variable is declared and initialized.

Applies to variables declared with let and const.
Helps catch errors by preventing access to variables before they're declared

console.log(x);
let x = 5; // ReferenceError: Cannot access 'x' before initialization


9. What is variable shadowing?
Variable shadowing occurs when a variable declared in a certain scope has the same name as a variable in an outer scope. 
The inner variable "shadows" the outer one, effectively hiding it.

let x = 10;

function exampleFuntion(){
    let x = 20; // this x shadows the outer x
    console.log(x); // 20
    if(true){
        let x = 30; // this x shadows both outer x variables
        console.log(x); // 30
    }
    console.log(x); // 20
}
exampleFunction();
console.log(x); // 10

10. What is a closure in JavaScript?
if any inner function holding the outer function data, then such scenario called as closure.

<script>
    function fun_one(){
        var x = 10;
        var y = 20;
        return ()=>{
            console.log(x);
            console.log(y);
        }
    };
    console.dir( fun_one() );  //0: Closure (fun_one) {x: 10, y: 20}
  
</script>


11. What are the different ways to define a function in JavaScript?

// Function declaration: hoisted and can be called before it's defined.
function great(name){
    return `hello, ${name}!`;
}

// Function expression: assigned to a variable, not hoisted
const greet = function(name){
    return `hello, ${name}!`;
};


//arrow function: shorter syntax, lexically binds 'this'
const greet = (name) => `hello, $ {name}!`;

//function constructor: creates a function dynamically
const greet = new Function("name", return `Hello, ${name}!`;");


12. What is a higher-order function?
A higher-order function is a function that treats other functions as data, either by taking them as arguments or returning them.

// Higher-order function that takes a function as an argument
function operate(x, y, operation){
    return operation(x, y); // calls the passed function with x and y
}

// function to be passed as arguments
const add = (a, b) => a + b; // arrow function for addition
const multiply = (a, b) => a * b; // arrow function for multiplication

//using higher order function
console.log(operate(5, 3, add)); // 8
console.log(operate(5,3, multiply)); // 15

13. Explain the concept of function hoisting?
Function hoisting is JavaScript's behavior of moving function declarations to the top of their scope during the compilation phase. 
This allows you to call a function before it appears to be defined in the code.

//this works due to hoisting
sayHello(); //output : "hello"

//function declaration is hoisted to the top of its scope
function sayHello(){
    console.log("hello!");
}

//note: function expressions are not hoisted
// hello(); // this would cause an error  --> ReferenceError: Cannot access 'hello' before initialization
// const hello = function(){console.log("hello");};

14. What is a pure function?
A pure function is a function that: Always returns the same output for the same inputs. 
Has no side effects (doesn't modify external state). Doesn't rely on external state. Make code more predictable and easier to test.

//pure function: always returns the same
//output for the same inputs
function add(a, b){
    return a + b; //deterministic and no side effects
}

// Impure function: modifies external state
let total = 0;
function addToTotal(value){
    total+= value; //modifies external variable 'total'
    return total;
}

15. What is the difference between function declaration and function expression?
Hoisting: Function declarations are hoisted, function expressions are not. 

Usage: Function declarations can be called before they appear in the code, function expressions cannot.

Naming: Function declarations require a name, function expressions can be anonymous.

// function declaration: hoisted and can be called before definition
sayHello(); // works due to hoisting
function sayHello(){
    console.log("hello");
}

// function expression: not hoisted, must be defined before use
// greet(); // error
const greet = function() {
    console.log("greetings");
};
greet(); // works when called after the expression.


16. What is an Immediately Invoked Function Expression (IIFE)?

An IIFE is a JavaScript function that runs as soon as it is defined.
// Arrow function with IIFE syntax
(()=>{
    console.log("Arrow function IIFE");
})();

//IIFE with parameters
(function(name){
    console.log(`hello, ${name}!`);
})("john");


17 How do you create an object in JavaScript?

//object literal notation
let person1 = {
    name : "vijay",
    age: 30,
    greet: function() {
        console.log(`hello, i'm {this.name}`);
    }
};

//constructor function
function Person(name, age){
    this.name = name;
    this.age = age;
    this.greet = function(){
        console.log(`hello, i'm ${this.name}`);
    };
}
let person2 = new Person("bob", 25);

-------------------------------------------
//object.create() method
let personProto = {
    greet: function() {
        console.log(`hello, i'm ${this.name}`);
    }
};
let person3 = Object.create(personProto);
person3.name = "charlie";
person3.age = 35;

//Es6 class syntax
class PersonClass {
    constructor(name, age){
        this.name = name;
        this.age = age;
    }
    greet(){
        console.log(`hello, i'm ${this.name}`);
    }
}
let person4 = new PersonClass("David", 40);

18 How do you add/remove properties to an object dynamically?

let car = {
    brand: "toyota",
    model: "corolla",
};

//adding properties
car.year = 2022; // dot notation
car["color"] = "blue"; //bracket notation

//removing properties
delete car.model; // removes the "model" property


19. How do you check if a property exists in an object?

let person = {
    name: "Alice",
    age: 30,
};

// using the in operator
console.log("name" in person); //true
console.log("job" in person); //false

// using hasOwnProperty method
console.log(person.hasOwnProperty("age")); // true
console.log(person.hasOwnProperty("city")); // false

// using undefined check
console.log(person.name !== undefined); // true
console.log(person.salary !== undefined); //false

// using Optional Chaining
console.log(person?.job); // undefined


20. What is the purpose of the this keyword in JavaScript?

The `this` keyword refers to the object that is executing the current function. Its value is determined by how a function is called.

// In a method
let person = {
    name: "alice",
    greet(){
        console.log(`hello, i'm ${this.name}`);
    },
};
person.greet(); //output: hello, i'm alice


// In an arrow function
let arrowGreet = () => {
    console.log(`hello, ${this.name}`);
};
arrowGreet.call({name: "charlie"}); 
// Output: hello, undefined (arrow functions don't bind their own 'this')

// In a constructor function
function Person(name){
    this.name = name;
    this.greet = function (){
        console.log(`hello, i'm ${this.name}`);
    };
}
let david = new Person("david");
david.greet(); //Output: hello, i'm david


21 What are the different ways to loop through an array in JavaScript?
1. for loop
2. for...in
3. for...of
4. map method(creates a new array)
5. while loop
6. do..while loop

example:
const fruits = ["apple", "banana", "orange", "mango"];

// 1.  for loop
for(let i =0; i < fruits.length; i++){
    console.log(fruits[i]);
}

// output: 
apple
banana
orange
mango

// 2. forEach method
fruits.forEach((fruit, index)=>{
    console.log(`${index}: ${fruit}`);
});

// output:
0: apple
1: banana
2: orange
3: mango

// 3. for... of loop(Es6+)
for(const fruit of fruits){
    console.log(fruit);
}

// output:
apple
banana
orange
mango

// 4. map method (creates a new array)
const upperFruits = fruits.map((fruit)=> fruit.toUpperCase());
console.log(upperFruits);
// Output:
[ 'APPLE', 'BANANA', 'ORANGE', 'MANGO' ]


// 5. while loop
let i = 0;
while(i < fruits.length){
    console.log(fruits[i]);
    i++;
}
// output:
apple
banana
orange
mango

// 6. do...while loop
let j = 0;
do {
    console.log(fruits[j]);
    j++;
} while(j < fruits.length);

// output
apple
banana
orange
mango


22. Explain the difference between for...in and for...of loops.

Key differences:
1. for...in iterates over all enumerable properties(including inherited ones)
2. for...of iterates over the values of an iterable object
3. for...in is generally used for objects, while for...of is used for arrays and other iterables

const fruits = ["apple", "banana", "orange"];
fruits.color = "mixed"; // adding a property to the array

// for...in loop(iterates over properties)
for(let index in fruits){
    console.log(index); 
} 

// output:
0
1
2
color

// for...of loop(iterates over iterable values)
for(let fruit of fruits){
    console.log(fruit);
}
// output:
apple
banana
orange


23. How do you add/remove elements from an array?

let fruits = ['apple', 'banana', 'orange'];

// adding elements
fruits.push('mango');
console.log(fruits);
// adds to the end: [ 'apple', 'banana', 'orange', 'mango' ]

fruits.unshift('grape');
console.log(fruits);
// adds to the beginiing: [ 'grape', 'apple', 'banana', 'orange', 'mango' ]

// removing elements
let lastFruit = fruits.pop();
console.log(fruits); // [ 'grape', 'apple', 'banana', 'orange' ]
// removes from the end: lastFruit = "mango"

let firstFruit = fruits.shift();
console.log(fruits); // [ 'apple', 'banana', 'orange' ]
// removes from the beginning: firstFruit = 'grape'

// adding/removing at specific index
fruits.splice(1, 0, 'kiwi');
console.log(fruits);  // [ 'apple', 'kiwi', 'banana', 'orange' ]
// adds 'kiwi' at index 1.

24. What is the purpose of the map() function? Es6 method
The map() method creates a new array with the results of calling a provided function on every element in the array.

const numbers = [1, 2, 3, 4, 5];

// using map to double each number
const doubledNumbers = numbers.map(num => num * 2);
console.log(doubledNumbers);  // [ 2, 4, 6, 8, 10 ]

// using map to create object from each number
const numberObjects = numbers.map(num => ({value: num, squared: num * num}));
console.log(numberObjects);
// Output:
[
  { value: 1, squared: 1 },
  { value: 2, squared: 4 },
  { value: 3, squared: 9 },
  { value: 4, squared: 16 },
  { value: 5, squared: 25 }
]

25. Explain the difference between filter() and find() methods. (ES6 methods)

Key differences:
1. filter() returns an array, find() returns a single element or undefined.
2. filter() checks all elements, find() stops at the first match.
3. filter() is used when you need all matching elements, find() when you need just the first match.

const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// filter(): returns a new array with all elements that pass the test
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [ 2, 4, 6, 8, 10 ]

// find(): returns the first element that satisfies the condition
const firstEvenNumber = numbers.find(num => num % 2 === 0);
console.log(firstEvenNumber); // 2

26. Explain the difference between some() and every() method.
some() method: Returns true if at least one element in the array satisfies the provided testing function. 
               Stops iterating as soon as it finds an element that satisfies the condition. 
               Returns false if no elements satisfy the condition.


every() method: Returns true if all elements in the array satisfy the provided testing function. 
                Stops iterating as soon as it finds an element that doesn't satisfy the condition.

const people = [
    {name: 'alice', age: 25 },
    {name: 'bob', age: 30},
    {name: 'charlie', age: 35}
];

// check if any person is over 30
const anyOver30 = people.some(person => person.age > 30);
console.log(anyOver30); // true (charlie is over 30)

// check if all people are over 20
const allOver20 = people.every(person => person.age > 20);
console.log(allOver20); // true (all are over 20)


27. How do you select elements in the DOM using JavaScript?

<div id = "myDiv" class="myClass">
    <p>First paragraph</p>
    <p>Second paragraph</p>
</div>

// select by ID
const divById = document.getElementById('myDiv');

// select by class name (returns a live HTMLCollection)
const elementByClass = document.getElementByClassName('myClass');

// select by tag name(returns a live HTMLCollection)
const paragraphs = document.getElementByTagName('p');

// select using CSS selectors (returns the first matching element)
const divBySelector = document.querySelector('#myDiv');

// select all matching elements using CSS selectors (returns a static NodeList)
const allParagraphs = document.querySelectorAll('p');

// using newer methods (less browser support)
const divByID = document.getElementById('myDiv');
console.log(divByID.querySelector('p')); // first <p> inside #myDiv
console.log(divByID.querySelectorAll('p')); // all <p> elemebts inside #myDiv 

28. How do you create and append elements to the DOM?

// create a new element
const newParagraph = document.createElement('p');

// set its content
newParagraph.textContent = "this is new paragraph.";

// add some attributes
newParagraph.id = "newPara";
newParagraph.className = "highlight";

// create a text node 
const textNode = document.createTextNode('Additional text.');

// append the text node to the paragraph
newParagraph.appendChild(textNode);

// append the new paragraph to an exisitng element
document.body.appendChild(newParagraph);

// alternative method using insertAdjacentHTML
const existingDiv = document.getElementById('existingDiv');
existingDiv.insertAdjacentHTML('beforeend', '<p>Inserted using unsertAdjacentHTML</p>');

29. Explain the difference between innerHTML and textContent.

Key differences:
innerHTML parses content as HTML, textContent does not
innerHTML can be slower and less secure (risk of XSS attacks)
textContent is generally faster and safer
innerHTML returns all content, including script and style element content
textContent returns the text content of all elements, ignoring tags

const div = document.createElement('div');

// innerHTML interprets the content as HTML
div.innerHTML = '<p>this is <strong>bold</strong> text</p>';
console.log(div.innerHTML);
// "<p>this is <strong>bold<strong> text<p>"

// textContent treats the content as plain text
div.textContent = '<p> this is <strong> bold</strong> text </p>';
console.log(div.textContent);
// "<p> this is <strong> bold </strong> text </p>"


30. How do you remove an element from the DOM?

<div id="parent"><p id="child">remove me</p></div>

// 1. method: using removeChild
const parent  = document.getElementById("parent");
const child = document.getElementById("child");
parent.removeChild(child);

// Method 2: using remove (newer, but less supported in older browsers)
const elementToRemove = document.getElementById("child");
elementToRemove.remove();

// Method 3: setting innerHTML to an empty string (removes all children)
document.getElementById("parent").innerHTML = "";

// Note: when removing elements, be sure to remove any associated event listeners
// to prevent memory leaks

31. What are arrow functions and how do they differ from regular functions?

key differences:
1. syntax: arrow functions have a more concise syntax.
2. "this" binding: arrow functions don't have their own "this"
3. No "arguments" object: arrow functions don't have the "argument" object


// arrow function
const addArrow = (a, b) => a + b;

// example of "this" binding difference
const obj = {
    name: "John",
    sayHello: function () {
        console.log("hello, " + this.name);
    },
    sayHelloArrow: () => {
        console.log("hello, " + this.name);
    },
};

obj.sayHello();
// output: hello, John

obj.sayHelloArrow();
// output: hello, undefined
// this refers to global/window object


32. Explain the concept of destructuring in JavaScript. ES6 concept
Destructuring is a way to extract multiple values from data stored in objects and arrays.

const person = {name: "alice" , age: 30, city: "new york"};

// old way
// const name = person.name;
// const age = person.age;

// destructuring
const {name, age, city} = person;
console.log(name, age, city); // alice 30 new york

// renaming variables
const { name: fullName, age: years } = person;
console.log(fullName, years); // alice 30

// array destructuring
const colors = ["red", "green", "blue"];

// Old way
// const firstColor = colors[0];
// const secondColor = colors[1];

// Destructuring
const [first, second, third] = colors;
console.log(first, second, third); // red green blue


33 What are template literals?
Template literals are string literals that allow embedded expressions and multi-line strings.

const nameVal = "alice";
const age = 30;

// old way
console.log("my name is " + nameVal + "and i'm" + age + "years old.");

// using tempalte literals
console.log(`my name is ${nameVal} and i'm ${age} years old.`); // my name is alice and i'm 30 years old.

// multi-line strings
const multiLine = `
this is a
multi-line
string
`;
console.log(multiLine); 
// output:
this is a
multi-line
string


34. How do you use the spread operator? Explain with example?
The spread operator (...) allows an iterable to be expanded in places where zero or more arguments or elements are expected.

// spreading arrays
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];
console.log(combined); // (6) [1, 2, 3, 4, 5, 6]

// spreading objects
const obj1 = {a: 1, b: 2};
const obj2= {c: 3, d: 4};
const mergeObj = {...obj1, ...obj2 };
console.log(mergeObj); // (4) {a: 1, b: 2, c: 3, d: 4}

// copying arrays
const original = [1, 2, 3];
const copy = [...original];
copy.push(4);
console.log(original, copy); //(3) [1, 2, 3] (4) [1, 2, 3, 4]

// spreading strings
const str = "hello";
const chars = [...str];
console.log(chars); //(5) ["h", "e", "l", "l", "o"]

35. What are default parameters in ES6?
Default parameters allow you to set default values for function parameters if no value or undefined is passed.

// using default parameters
function greetES6(name = "guest"){
    console.log(`hello, ${name}!`);
}
greetES6(); // hello, guest!
greetES6("alice"); // hello, alice!

// default parameters with expressions
function multiply(a, b = a * 2){
    return a * b;
}
console.log(multiply(5)); // 50
console.log(multiply(5, 3)); // 15

36. How do you use the rest parameter in functions?
The rest parameter syntax allows a function to accept an indefinite number of arguments as an array.

//using rest parameter
function sumES6(...numbers){
    return numbers.reduce((total, num)=> total + num, 0)
}

console.log(sumES6(1, 2, 3, 4, 5)); // 15


// rest parameter with other parameters
function multiply(multiplier, ...numbers){
    return numbers.map((num)=> multiplier * num);
}
console.log(multiply(2,1,2,3,4)); // (4) [2, 4, 6, 8]

// object rest properties
const { a, b, ...rest} = { a: 1, b: 2, c: 3, d: 4};
console.log(a,b, rest); // 1 2 (2) {c: 3, d: 4}

//array rest elements
const [first, second, ...others] = [1, 2, 3, 4, 5];
console.log(first, second, others); // 1 2 (3) [3, 4, 5]

// rest parameters in arrow functions
const logAll = (...args) => console.log(args);
logAll(1, 2, 3, "four", {five: 5}); //(5) [1, 2, 3, "four", {...}]

37. What is callback & callback hell explain with example?
Callbacks are functions passed as arguments to other functions, often used for asynchronous operations. 
Callback hell occurs when multiple nested callbacks make code hard to read and maintain.

// simple callback example
function greet(name, callback){
    //simulate an async operation
    setTimeout(()=>{
        console.log(`hello, ${name}!`);
        callback();
    }, 1000);
}

// using the callback
greet("alice", ()=>{
    console.log("greeting finished");
});
// output:
hello, alice!
greeting finished

// Callback hell example
function step1(callback){
    setTimeout(()=>{
        console.log("step 1");
        callback();
    }, 1000);
}

function step2(callback){
    setTimeout(()=>{
        console.log("Step 2");
        callback();
    }, 1000)
}

// callback hell
step1 (()=>{
    step2(()=>{
        console.log("Done");
    });
});

// output
step 1
Step 2
Done

38. What is a Promise in JavaScript with example?
A Promise is an object representing the eventual completion or failure of an asynchronous operation.

// Promise example
function fetchData() {
    return new Promise((resolve, reject)=>{
        setTimeout(()=>{
            const success = true;
            if(success){
                resolve("data fetched successfully");
            } else {
                reject("error fetching data");
            }
        }, 1000);
    });
}

fetchData().then((data)=> console.log(data))
.catch((error)=> console.error(error));
// output: data fetched successfully


39. How do you chain Promises?
Promise chaining allows you to perform sequential asynchronous operations.

function step1(){
    return Promise.resolve("step 1 complete");
}

function step2(prevResult){
    return Promise.resolve(`${prevResult}, step 2 complete`);
}

step1()
    .then((result) => step2(result))
    .then((finalResult)=> console.log(finalResult))
    .catch((error)=> console.error(error));

    // output: step 1 complete, step 2 complete

40. What is the purpose of the Promise.all() method?
Promise.all() takes an iterable of promises and returns a single Promise that resolves when all input promises have resolved, or rejects if any input promise rejects.

const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve)=> setTimeout(()=> resolve(42), 100));

Promise.all([promise1, promise2])
.then((values)=> console.log(values))    // (2) [3, 42]
.catch((error)=> console.error(error));


41. What is the purpose of the finally() method in Promises?
The finally() method is used to specify code that should be executed regardless of whether the promise is fulfilled or rejected.

function fetchData(){
    return new Promise((resolve, reject)=>{
        const success = Math.random() > 0.5;
        setTimeout(()=>{
            if(success){
                resolve("data successfully fetched");
            } else {
                reject("Error: failed to fetch data");
            }
        }, 1000);
    });
}

fetchData()
    .then((result)=>{
        console.log(result);
    })
    .catch((error)=>{
        console.error(error);
    })
    .finally(()=>{
        // this block always run, regardless of fulfillment or rejection
        console.log("operation completed. loading status:");
    });

    //output:
    Error: failed to fetch data
    operation completed. loading status:


42 What is the purpose of the async await ?
The purpose of async/await is to simplify the syntax for working with Promises, making asynchronous code easier to write and read. 
It allows you to write asynchronous code that looks and behaves more like synchronous code.

// function that returns a promise
function fetchData() {
    return new Promise((resolve)=>{
        setTimeout(()=> resolve("data fetched"), 2000);
    });
}

// using async/await
async function getData() {
    console.log("fetching data...");
    const result = await fetchData();
    console.log(result);
    console.log("Data processing complete");
}

getData();

// output:
fetching data...
data fetched
Data processing complete

43. How do you handle errors in async/await?

async function fetchUserData(userId){
    try {
        const response = await fetch(`https://api.example.com/users/${userId}`);
        if(!response.ok){
            throw new Error('Failed to fetch user data');
        }
        const userData = await response.json();
        console.log(userData);
    } catch (errror){
        console.error("error:", error.message);
    }
}

fetchUserData(123);


44. What is the difference between async/await and Promises?
Syntax: Async/await provides a more linear, synchronous- looking code structure.
Error handling: Async/await uses try/catch, which is more familiar for synchronous code.
Chaining: Promises use .then() for chaining, while async/await uses regular JavaScript control flow.
Debugging: Async/await can be easier to debug as it behaves more like synchronous code


45. What is the difference between default and named exports?
A module can have multiple named exports but only one default export.
Named exports are imported using curly braces, while default exports are imported without them.
Default exports can be imported with any name, while named exports must be imported with their exact names (unless renamed using `as`).

// named exports
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;

// default export
export default function multiply(a, b) {
    return a * b;
}

// importing named exports
import { add, subtract} from "./math.js";

// importing default export
import multiply from "./math.js; // it can be import vijay

console.log(add(5, 3)); // 8
console.log(subtract(10, 4)); // 6
console.log(multiply(2, 3)); // 6


46. How do you convert a JavaScript object to a JSON string ?

const user = {
    name: "john doe",
    age: 30,
    isAdmin: false,
};

const jsonString = JSON.stringify(user);
console.log(jsonString);
// Output: {"name":"john doe","age":30,"isAdmin":false}


47. How do you parse a JSON string back into a JavaScript object?

const jsonString = '{"name":"john doe","age":30,"isAdmin":false}';

const user = JSON.parse(jsonString);
console.log(user.name); // john doe
console.log(user.age); // 30
console.log(user.isAdmin); //false


48. What is localStorage in JavaScript, and how do you store and retrieve data from it?
localStorage is a web storage object that allows you to store key-value pairs in the browser with no expiration time.

// storing data
localStorage.setItem('username', 'vijay');
localStorage.setItem('isLoggedIn', 'true');

// retrieving data
const username = localStorage.getItem('username');
console.log(username); //vijay

const isLoggedIn = localStorage.getItem('isLoggedIn') === 'true';
console.log(isLoggedIn); // true

// storing and retrieving objects
const user = {name: 'John', age: 30};
localStorage.setItem('user', JSON.stringify(user));

const storedUser = JSON.parse(localStorage.getItem('user'));
console.log(storedUser.name); // John

49. What is the difference between localStorage and sessionStorage?
Both localStorage and sessionStorage are web storage objects, but they differ in data persistence.
localStorage data persists even after the browser is closed and reopened. 
sessionStorage data is cleared when the page session ends (i.e., when the tab is closed).
Both have the same API and are limited to storing string data.

// localstorage: persists even after the browser window is closed.
localStorage.setItem(
    "persistentData", 
     "This will remain after closing the browser"
);

// session storage: data is cleared when the browser session ends
sessionStorage.setItem(
    "temproraryData",
    "This will be cleared when the session ends"
);

// both are used similarly
console.log(localstorage.getItem("persistentData"));
console.log(sessionStorage.getItem("temporaryData"));

50. How do you delete a specific item from localStorage or clear all data from it?

// storing some data
localStorage.setItem("username", "JohnDoe");
localStorage.setItem("isLoggedIn", "true");

// removing a specific item
localStorage.removeItem("isLoggedIn");

console.log(localStorage.getItem("username")); //JohnDoe
console.log(localStorage.getItem("isLoggedIn")); // null

// clearing all data from localstorage
localStorage.clear();
sessionStorage.clear();

console.log(localStorage.getItem("username")); // null
