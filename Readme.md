# Javascript interview questions & answers

Credit: [Front-end-Developer-Interview-Questions/javascript-questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/javascript-questions.md)

### 1. Explain event delegation

Event delegation is a way to handle events that happen on multiple elements at once, by using a single event handler on a parent element.


First example: Imagine you have a basket of apples, and you want to know when one of the apples is picked. Instead of putting a separate tag on each apple, you can put a tag on the basket and when someone picks an apple, the basket will know.

In the same way, on a website, you can have a lot of buttons, and you can put an event listener on the parent element (like a container) and check which button was clicked.

This way you can handle many elements with a single event handler, and it also makes it easier to add or remove elements from the website, because you don't have to add or remove event handlers each time you change the website.

So, event delegation is like having a basket with many apples, and you put a tag on the basket instead of each apple, so you know when an apple is picked. On a website, it's like having many buttons, and you put an event listener on the parent element instead of each button, so you know which button was clicked. <—

Event delegation is a way to handle events in JavaScript that allows you to add an event listener to a parent element, rather than adding individual event listeners to multiple child elements.

Second example: Imagine you have a toy box with a bunch of toy cars inside. You want to be able to make the toy cars move when you press a button, but you don't want to add a button to each individual toy car. Instead, you can add a single button to the toy box, and use event delegation to handle the button press.

Here's how you could do this in JavaScript:

In this example, we add an event listener to the **`toyBox`** element that listens for clicks. When a click occurs, the event listener checks to see if the element that was clicked (the **`event.target`**) is a toy car (has a class of **`toy-car`**). If it is, the toy car's class is updated to include the **`moving`** class, which can be used to apply a moving animation to the toy car.

By using event delegation, we can add a single event listener to the toy box, rather than having to add a separate event listener to each toy car. This can be more efficient and easier to manage, especially if the number of toy cars changes over time.

```markdown
const toyBox = document.querySelector('.toy-box');

toyBox.addEventListener('click', function(event) {
  if (event.target.matches('.toy-car')) {
    event.target.classList.add('moving');
  }
});
```

### 2. Explain how 'this' keyword works in JavaScript

In JavaScript, the **`this`** keyword is a special word that refers to the object that is currently being used. It's like a way to access properties and methods of an object from inside the object itself.

Here's an example:

Imagine you have a toy box with some toys inside. The toy box is an object, and the toys are the properties and methods of the object. The **`this`** keyword is like a special pointer that points to the toy box and helps you reach the toys inside.

Here's how you could use the **`this`** keyword to play with the toys:

In this example, the **`play`** method uses the **`this`**keyword to access the **`toy1`** and **`toy2`**
 properties of the **`toyBox`**object. When we call the **`play`** method on the **`toyBox`**object (**`toyBox.play()`**), the value of **`this`** is set to the **`toyBox`**object.

```markdown
const toyBox = {
  toy1: 'teddy bear',
  toy2: 'doll',
  play: function() {
    console.log(`Playing with my ${this.toy1} and my ${this.toy2}`);
  }
}

toyBox.play();  // Output: "Playing with my teddy bear and my doll"

```

**2.1 Can you give an example of one of the ways that working with 'this' has changed in ES6?**

In ES6 (also known as ECMAScript 2015), the way that the **`this`** keyword works inside arrow functions is different than it is in regular functions.

Here's an example that demonstrates the difference:

In this example, the **`greet`** method uses the **`this`** keyword to access the **`name`** property of the **`person`** object, as expected. However, when we call the **`greetArrow`** method, the value of **`this`** is not set to the **`person`** object, as it is in the **`greet`** method.

This is because arrow functions do not have their own **`this`** value. The value of **`this`** inside an arrow function is determined by the context in which the function is called. In this case, the value of **`this`** is set to the global object (**`window`** in the browser), because the **`greetArrow`** function is called as a standalone function, not as a method of an object.

```jsx
const person = {
  name: 'Alice',
  age: 30,
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  },
  greetArrow: () => {
    console.log(`Hello, my name is ${this.name}`);
  }
}

person.greet();  // Output: "Hello, my name is Alice"
person.greetArrow();  // Output: "Hello, my name is undefined"
```

### 3. Explain how prototypal inheritance works.

In JavaScript, prototypal inheritance is a way for one object to inherit properties and methods from another object. It's a way to create a relationship between objects, where one object is the "parent" and the other object is the "child."

Here's an example of how prototypal inheritance works in JavaScript

```jsx
const animal = {
  type: 'animal',
  makeSound: function() {
    console.log('Some generic animal sound');
  }
}

const dog = Object.create(animal);
dog.type = 'dog';
dog.makeSound = function() {
  console.log('Woof woof');
}

const cat = Object.create(animal);
cat.type = 'cat';
cat.makeSound = function() {
  console.log('Meow');
}

animal.makeSound();  // Output: "Some generic animal sound"
dog.makeSound();  // Output: "Woof woof"
cat.makeSound();  // Output: "Meow"
```

In this example, the **`animal`** object is the parent object, and the **`dog`** and **`cat`** objects are the child objects. The **`dog`** and **`cat`** objects are created using the **`Object.create()`** method, which creates a new object and sets its prototype to the object passed as an argument (in this case, the **`animal`** object).

This means that the **`dog`** and **`cat`** objects have access to the properties and methods of the **`animal`** object. However, they can also have their own properties and methods, which override the ones inherited from the parent object.

In this example, the **`dog`** and **`cat`** objects both have a **`makeSound`** method, which overrides the **`makeSound`** method of the **`animal`** object. When we call the **`makeSound`** method on the **`dog`** and **`cat`** objects, their own version of the method is called, rather than the one inherited from the **`animal`** object.

### 4. What's the difference between a variable that is: `null`, `undefined` or undeclared?

In programming, a variable is a place to store a value. However, sometimes a variable might not have a value at all, or it might not even exist. Here is the difference between a variable that is null, undefined, or undeclared:

- A variable that is null is a variable that has been defined and has the value of null, which means "no value." This can be done intentionally, for example to clear the value of a variable that was previously set to something else.
- A variable that is undefined is a variable that has been defined, but has not been given a value. This can happen if you define a variable but forget to give it a value, or if you try to access a variable that doesn't exist.
- A variable that is undeclared is a variable that has not been defined at all. This can happen if you try to use a variable before you have declared it, or if you mistyped the name of a variable.

### 5. What is a closure, and how/why would you use one?

A closure is a function that remembers the variables and context in which it was created. It has access to these variables even when it is executed outside of its original scope.

Closures are often used to create functions that can be passed around and executed at a later time, while still having access to the variables and context in which they were created. They can be used to create callback functions or event handlers, or to create functions with private variables that can only be accessed by the inner function.

```jsx
function makeCounter() {
  let count = 0;

  // The function below is a closure. It has access to the variable count,
  // even though it is executed outside of the function where count is defined.
  function increment() {
    count++;
    console.log(count);
  }

  return increment;
}

let counter = makeCounter();
counter();  // Output: 1
counter();  // Output: 2
counter();  // Output: 3
```

### 6. What language constructions do you use for iterating over object properties and array items?

In JavaScript, there are several language constructs that can be used for iterating over object properties and array items. Here are some examples:

• For...in loop: This loop iterates over the properties of an object.

• For...of loop: This loop iterates over the values of an iterable object, such as an array.

• Array.forEach() method: This method iterates over the elements of an array and executes a callback function for each element.

### 7. Can you describe the main difference between the `Array.forEach()` loop and `Array.map()` methods and why you would pick one versus the other?

In JavaScript, the **`Array.forEach()`** and **`Array.map()`** methods are both used to iterate over the elements of an array and transform the elements in some way. However, there are some key differences between these two methods:

- The **`Array.forEach()`** method is used to iterate over an array and perform a function on each element, but it does not return a new array. It is generally used for side effects, such as updating the UI or logging to the console.

```
const array = [1, 2, 3];

array.forEach(value => {
  console.log(value * 2);
});

// Output:
// 2
// 4
// 6
```

• The **`Array.map()`** method is used to iterate over an array, transform each element, and return a new array with the transformed elements. It is generally used to create a new array from an existing array.

```jsx
const array = [1, 2, 3];

const doubled = array.map(value => {
  return value * 2;
});

console.log(doubled);  // Output: [2, 4, 6]
```

In general, you would use the **`Array.forEach()`**
 method when you want to iterate over an array and perform a function on each element, but you don't need to return a new array. You would use the **`Array.map()`**
 method when you want to transform the elements of an array and return a new array with the transformed elements.

### 8. What's a typical use case for anonymous functions?

Anonymous functions are functions that are not bound to a name. They are often used as inline functions, or as arguments to other functions.

One typical use case for anonymous functions is as callback functions. A callback function is a function that is passed as an argument to another function, and is executed after the outer function has completed some task. Anonymous functions are often used as callback functions because they do not need to be named, and they can be defined and passed as arguments at the same time.

Here is an example of an anonymous function being used as a callback function:

```jsx
setTimeout(function() {
  console.log("I am a callback function");
}, 1000);
```

In this example, the anonymous function is passed as an argument to the **`setTimeout()`** function, which executes the function after a specified delay.

Anonymous functions are also often used as event handlers, such as in this example:

```
document.addEventListener("click", function() {
  console.log("The document was clicked");
});
```

In this example, the anonymous function is passed as an argument to the **`addEventListener()`**
 method, and it is executed when the "click" event is triggered on the document.

### 9. What's the difference between host objects and native objects?

In JavaScript, host objects are objects provided by the host environment (e.g. the web browser) that are used to expose functionality or resources to JavaScript code. Native objects are objects that are part of the JavaScript language and are provided by the JavaScript runtime.

Here are some examples of host objects:

- **`window`**: The **`window`** object is a host object that represents the current web browser window, and provides access to the browser's functionality and resources.
- **`XMLHttpRequest`**: The **`XMLHttpRequest`** object is a host object that is used to send HTTP requests and receive responses from a server.
- **`HTMLDivElement`**: The **`HTMLDivElement`** object is a host object that represents an HTML **`div`** element, and provides access to the properties and methods of the element.

Here are some examples of native objects:

- **`Array`**: The **`Array`** object is a native object that represents an ordered collection of values, and provides methods for manipulating and iterating over the values.
- **`String`**: The **`String`** object is a native object that represents a string value, and provides methods for manipulating and querying the value.
- **`Math`**: The **`Math`** object is a native object that provides mathematical functions and constants.

In general, host objects are specific to the host environment in which the JavaScript code is running, while native objects are part of the JavaScript language and are available in any JavaScript environment.

### 10. Explain the difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?

In JavaScript, there are several ways to create functions and objects, and the way in which you create them can have different effects on the resulting objects and their behavior.

Here is an explanation of the difference between the three statements you provided:

- **`function Person(){}`**: This statement defines a function called **`Person`**. The function can be called by its name, and it can be used to create objects.
- **`var person = Person()`**: This statement calls the **`Person`** function and assigns the returned value to the **`person`** variable. If the **`Person`** function does not return a value, the **`person`** variable will be assigned the value **`undefined`**.
- **`var person = new Person()`**: This statement creates a new object using the **`Person`** function as a constructor. The **`new`** operator creates an empty object, and then calls the **`Person`** function with the **`this`** keyword set to the new object. The **`Person`** function can then add properties and methods to the object, and the object is returned as the result of the **`new Person()`** expression.

Here is an example that demonstrates the difference between these three statements:

```
function Person() {
  this.name = "John";
  this.sayHi = function() {
    console.log(`Hi, my name is ${this.name}`);
  }
}

var person1 = Person();  // Calls the Person function
console.log(person1);  // Output: undefined

var person2 = new Person();  // Creates a new object using the Person function as a constructor
console.log(person2.name);  // Output: "John"
person2.sayHi();  // Output: "Hi, my name is John"

```

### 11. Explain the differences on the usage of `foo` between `function foo() {}` and `var foo = function() {}`

In JavaScript, there are two ways to define a function: as a function declaration, or as a function expression.

There are two ways to define a function in JavaScript: as a function declaration or as a function expression.

Function declarations are defined using the **`function`** keyword, followed by a name and a function body. They are hoisted to the top of the current scope, which means that they are available for use throughout the entire scope, even before the declaration appears in the code. They are not subject to variable hoisting, which means that they cannot be reassigned to a different value.

Function expressions are defined using the **`function`** keyword, followed by a function body, and are assigned to a variable. They are not hoisted, and are only available after the expression has been evaluated. They can be reassigned to different values.

Here is an example that demonstrates the difference between function declarations and function expressions:

```

foo();  // Output: "I am a function"

function foo() {
  console.log("I am a function");
}

bar();  // Output: Uncaught TypeError: bar is not a function

var bar = function() {
  console.log("I am a function expression");
};

```

### 12. Can you explain what `Function.call` and `Function.apply` do? What's the notable difference between the two?

In JavaScript, the **`Function.call()`** and **`Function.apply()`** methods allow you to call a function with a specific **`this`** value and arguments.

The **`Function.call()`** method is used to call a function with a specific **`this`** value and arguments passed to the function as separate parameters. It has the following syntax:

```jsx
function.call(thisValue, arg1, arg2, ...);
```

Here is an example of how to use the **`Function.call()`** method:

```jsx
function greet(greeting) {
  console.log(`${greeting}, my name is ${this.name}`);
}

const person = { name: "John" };

greet.call(person, "Hello");  // Output: "Hello, my name is John"
```

The **`Function.apply()`** method is similar to the **`Function.call()`** method, but it allows you to pass the arguments to the function as an array. It has the following syntax:

```jsx
function.apply(thisValue, [arg1, arg2, ...]);
```

Here is an example of how to use the **`Function.apply()`** method:

```jsx
function greet(greeting) {
  console.log(`${greeting}, my name is ${this.name}`);
}

const person = { name: "John" };

greet.apply(person, ["Hello"]);  // Output: "Hello, my name is John"
```

The main difference between the **`Function.call()`** and **`Function.apply()`** methods is the way in which the arguments are passed to the function. The **`Function.call()`** method requires the arguments to be passed as separate parameters, while the **`Function.apply()`** method requires the arguments to be passed as an array.

### 13. Explain `Function.prototype.bind`.

In JavaScript, the **`Function.prototype.bind()`** method allows you to create a new function that is bound to a specific **`this`** value and arguments. It has the following syntax:

```jsx
function.bind(thisValue, arg1, arg2, ...);
```

The **`bind()`** method creates a new function that, when called, has its **`this`** keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

Here is an example of how to use the **`bind()`** method to create a new function that is bound to a specific **`this`** value and arguments:

```jsx
function greet(greeting, exclamation) {
  console.log(`${greeting}, my name is ${this.name}${exclamation}`);
}

const person = { name: "John" };

const sayHello = greet.bind(person, "Hello", "!");

sayHello();  // Output: "Hello, my name is John!"
```

In this example, the **`bind()`** method creates a new function called **`sayHello`** that is bound to the **`person`** object as the **`this`** value and the arguments "Hello" and "!". When the **`sayHello()`** function is called, it logs the string "Hello, my name is John!" to the console.

The **`bind()`** method is often used to bind a function to a specific **`this`** value when passing the function as a callback or to create a partial function that pre-fills some of the arguments.

### 14. What's the difference between feature detection, feature inference, and using the UA string?

When developing for the web, you often need to know what features are available in the user's browser in order to provide an optimal experience. There are several ways to determine which features are available, each with their own advantages and disadvantages. These include feature detection, feature inference, and using the user agent (UA) string.

1. Feature Detection:
Feature detection is a technique where you directly check for the existence of a specific feature or API. This is done by running a specific test for that feature and checking its return value. The advantage of feature detection is that it will work correctly even if the user has a modified UA string or the feature is available on a browser that doesn't identify itself as you expect.
2. Feature Inference:
Feature inference is a technique where you check for the existence of a related feature or API, and infer that the feature you're looking for is also available. This technique is less reliable than feature detection, as it relies on certain assumptions about the existence of certain features. Feature inference can be useful when feature detection is not possible or practical.
3. Using the UA string:
Another way to detect browser feature support is to check the user agent (UA) string. This is the string of text that a browser sends to a server with each request. UA strings often include information about the browser and its version, which can be used to determine which features are available. However, this approach is not very reliable because the UA string can be easily spoofed, and it does not take into account any changes to the user's browser.

In general, feature detection is considered the best practice when checking for feature support, as it directly tests for the existence of a specific feature, without making any assumptions. However, depending on the feature you're trying to detect, you might use a combination of all three method, or even use another one.

### 15. Explain "hoisting".

"Hoisting" is a term used in JavaScript to describe the behavior of variable and function declarations being moved to the top of their scope.

Imagine you have a toy box, where you keep all your toys. Inside the toy box, you have different compartments for different types of toys. You have a compartment for stuffed animals, one for action figures, and one for blocks.

When you want to play with one of the toys, you reach inside the toy box and grab it. Similarly, in JavaScript, when you want to use a variable or a function, the computer will "look" for it in the right "compartment" (scope).

But with hoisting, it's like the toys are "magically" being lifted to the top of the toy box so they are easier to grab. In JavaScript, when you write a variable or function declaration, it's being "lifted" to the top of their scope, so they are easier to reach and use. This means that you can use a variable or call a function before you declare it in your code.

This behavior can be confusing especially for beginners, and it's often recommended to always declare all variables at the top of their scope to avoid any surprises and unexpected bugs.

### 16. Describe event bubbling.

Event bubbling is a term used in JavaScript to describe how events move through the HTML elements on a webpage.

Imagine you are blowing bubbles in the park with your friends. Each bubble you blow goes up in the air and floats around. When one bubble comes in contact with another, they stick together and become one big bubble.

Similarly, in JavaScript, when you click on an element on a webpage, like a button, it creates an "event" (kind of like a bubble). This event will then move up through all the parent elements that contain it. Like when bubble come in contact and make one big bubble, the events on the page travel up through the parent elements, making all elements that contain it aware of the event, this process is called event bubbling.

This process can be useful in some cases because it allows you to listen for events on multiple elements at once, for example, you can listen for a click event on a button and its parent container, allowing you to handle the click event in different ways.

But it can also be a source of confusion, especially when you want to handle an event on a specific element, in this case, you have to make sure to stop the event from "bubbling up" to the parent elements by using a method called event.stopPropagation()

### 17. Describe event capturing.

Event capturing is a term used in JavaScript to describe how events move through the HTML elements on a webpage in the opposite direction of event bubbling.

Imagine you are playing catch with a ball in a field, and there are different layers of people between you and the person you are throwing the ball to. You throw the ball, and it first goes through the people who are closest to you, and then it goes through the people who are further away, until it reaches the person you are throwing it to.

Similarly, in JavaScript, when you click on an element on a webpage, like a button, it creates an "event" (kind of like the ball). This event will then move down through all the child elements that are inside the element that you clicked on, in the opposite direction of event bubbling.

This process is called event capturing, and it allows you to handle an event on a specific element, before it reaches the element that was actually clicked on. Event capturing is not as commonly used as event bubbling, but it can be useful in some cases, for example, when you want to handle an event on multiple nested elements, but in a specific order.

Just like when you are playing catch and you want the ball to go to a specific person, in JavaScript you can specify which elements you want to handle the event first by using a method called addEventListener and setting the 3rd parameter as true, this will make the event go through capturing phase first, before bubbling.

### 18. What's the difference between an "attribute" and a "property"?

In JavaScript, when you are working with HTML elements, you might come across the terms "attribute" and "property". These terms are often used interchangeably, but they refer to different things.

An "attribute" is a value that is set on an HTML element in the markup (e.g., the HTML source code) of a webpage. For example, if you have an **`input`** element with the attribute **`value`** set to "hello", the HTML for this would look like this: **`<input value="hello">`**.

A "property" on the other hand, is a value that is associated with an element and can be accessed and modified through the JavaScript API. When the browser renders the page, it takes the attribute and assigns it to the corresponding property of the JavaScript object representing the element. For example, the following code accesses the "value" property of an input element, which corresponds to the "value" attribute in the HTML.

```jsx
let input = document.querySelector("input");
console.log(input.value);
```

In summary, an attribute is a value that is set on an HTML element in the markup of the page, while a property is a value that is associated with an element and can be accessed and modified through JavaScript.

It's important to note that sometimes the attribute and property may have different values, for example, when you set a value to an element property programmatically, it will change the corresponding attribute, but if you change the attribute value directly via HTML, the property value remain the same unless you refresh the page.

### 19. What are the pros and cons of extending built-in JavaScript objects?

Sometimes, people like to add new things to things that already exist in JavaScript, like the Array or String objects. This is called "extending" the built-in objects.

There are some good things and some bad things about doing this.

The good things are:

- You can add new features that you think are missing in the built-in objects.
- You can make your code shorter and more readable by using the new features that you've added.

The bad things are:

- It can make your code harder to understand for other people who might read it.
- If you add something new to a built-in object, other people's code might not work well with yours.
- It can also lead to naming conflicts, where your new feature has the same name as something that already existed.
- It can be a bad practice, and it's not recommended by the javascript community.

So, when you think about extending built-in JavaScript objects, it's important to weigh the pros and cons and make sure you're doing it for the right reasons. It's better to use your own custom objects or use libraries that provide the functionality you need and avoid extending the built-in objects.

### 20. What is the difference between `==` and `===`?

The **`==`** operator, also known as the "loose equality" or "abstract equality" operator, compares two values for equality after converting them to a common type. For example, if you compare a number and a string with the same value (e.g., **`3 == "3"`**), the operator will return **`true`** because JavaScript will convert the string to a number before making the comparison.

The **`===`** operator, also known as the "strict equality" or "identity" operator, compares two values for equality without converting them to a common type. This means that it compares the values and their types. For example, if you compare a number and a string with the same value using this operator (e.g., **`3 === "3"`**), the operator will return **`false`** because the values have different types.

Here's an example:

```jsx
0 == false // true
0 === false // false
```

In this example, 0 and false are equivalent, but they are not of the same type, that's why 0 == false returns true, but 0 === false returns false.

In general, it's considered best practice to use the **`===`** operator, because it compares values and their types, avoiding unexpected behavior and bugs when comparing different types. However, there are some situations where **`==`** is useful, such as when you want to compare values that have different types but should be treated as equal.

### 20. Explain the same-origin policy with regards to JavaScript.

The same-origin policy is a rule that helps to keep the information on your website safe. It says that a website can only access information from other websites if those websites are from the same place.

Imagine that your website is a big house, and all the other websites are other big houses. The same-origin policy says that people from your house can only go into other houses if they're from the same neighborhood.

For example, if your website is "**[www.mywebsite.com](http://www.mywebsite.com/)**", it can only access information from other websites that are also "**[www.mywebsite.com](http://www.mywebsite.com/)**". It can't access information from "**[www.otherwebsite.com](http://www.otherwebsite.com/)**" or "**[www.notmywebsite.com](http://www.notmywebsite.com/)**" unless they specifically allow it.

This helps to protect you and your visitors from bad websites that might try to steal your information or do something harmful. The same-origin policy is one of the ways that your web browser helps to keep you safe online.

### 21.  Why is it called a Ternary operator, what does the word "Ternary" indicate?

The word "ternary" comes from the Latin word "ternarius" which means "composed of three parts" .

In programming, a Ternary operator is called so because it is composed of three parts. It is a shorthand way of writing an **`if-else`** statement, and it takes the form of **`(condition) ? (if true) : (if false)`**. It is a shorthand way of writing if-else statement and it's often called a shorthand of if-else statement.

The Ternary operator is a compact and simple way of writing an if-else statement, It's a shorthand way of expressing a simple branching statement that assigns the value of one expression to a variable depending on the boolean value of another expression

In short, Ternary operator is called so because it is composed of three parts: a condition, a value to return if the condition is true, and a value to return if the condition is false.

### 22. What is strict mode? What are some of the advantages/disadvantages of using it?

Strict mode is a feature in JavaScript that enables "strict" error checking and changes the behavior of certain language features. When strict mode is enabled, it catches some common coding mistakes and makes them throw errors, instead of silently failing or producing unpredictable results.

You can enable strict mode for an entire JavaScript file by adding the string "use strict" at the top of the file, or for an individual function by adding "use strict" as the first statement in the function.

Advantages of using strict mode include:

- It catches errors that would have been silently ignored and makes them throw an error, making it easier to find and fix bugs.
- It helps prevent accidental global variable declarations by throwing an error when you try to assign a value to an undeclared variable
- It makes it impossible to use certain keywords as variable or function names.
- It makes the code more secure and less prone to common coding mistakes.

Disadvantages of using strict mode include:

- It might break existing code that relies on the behavior of non-strict code.
- It might make code harder to understand for developers who are not familiar with strict mode.
- It can be more difficult to debug as it throws an error when it finds an issue, instead of silently failing.

Overall, strict mode is a feature that can help you write more robust, maintainable and secure code. However, it's important to weigh the advantages and disadvantages and decide whether strict mode is the best option for a specific project and development team.

### 23. What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?

Advantages:

- Stronger typing: Some languages that compile to JavaScript, like TypeScript, have built-in support for strong typing, which can help catch errors early and make the code more robust. This means that variables have specific types (such as number or string) and the compiler will check that you are using them correctly.
- Better tooling: Some languages that compile to JavaScript, like CoffeeScript, provide a more concise and expressive syntax, which can make the code more readable and easier to write. This can also lead to more efficient and less error-prone code.
- Access to new features: Some languages that compile to JavaScript, like Dart, provide access to features that are not available in JavaScript, such as classes and interfaces.
- Better performance: Some languages that compile to JavaScript, like Dart, provide better performance than JavaScript, by providing features such as ahead-of-time (AOT) compilation and garbage collection.

Disadvantages:

- Extra setup: In order to use a language that compiles to JavaScript, you'll need to set up a build process, which can be complex and time-consuming. This can include installing and configuring additional tools and libraries.
- Extra Learning: Developers need to learn a new language and its syntax, which can take time and effort.
- Browser support: Some languages that compile to JavaScript, like Dart, may not be supported by all browsers, which can limit the reach of your application.
- Additional complexity: The use of a language that compiles to JavaScript can add an additional layer of complexity to the development process.
- Browser compatibility issues: The generated javascript code may not be compatible with all browsers and versions, which can create compatibility issues.

In summary, the use of a language that compiles to JavaScript can provide advantages such as better typing, tooling, and performance. However, it also introduces additional setup, learning, and compatibility issues that should be considered. Whether or not to use a language that compiles to JavaScript depends on the specific needs of your project and the trade-offs you are willing to make.

### 24. What tools and techniques do you use debugging JavaScript code?

There are several tools and techniques that can be used to debug JavaScript code, some of the most commonly used are:

1. Console: The JavaScript console provides a way to log information and interact with the JavaScript runtime. You can use the **`console.log()`** function to print information to the console, as well as other methods such as **`console.error()`**, **`console.warn()`**, **`console.info()`** and **`console.debug()`**. This can be useful for printing out variables, tracking down errors and verifying the behavior of code at different points in the execution.
2. Debugger statement: The **`debugger`** statement allows you to stop the execution of JavaScript code at a specific point. When a browser's developer console is open and connected to a page, execution will stop at the **`debugger`** statement, allowing you to inspect the state of the variables, call stack, and other information in the scope at that point.
3. Browser DevTools: Most modern web browsers have built-in developer tools that allow you to inspect and debug JavaScript code. These tools provide features such as a JavaScript console, a call stack, a scope and variable viewer, and a way to set breakpoints and step through code.
4. Breakpoints: One of the most powerful features in debugging is the ability to set breakpoints in the code. A breakpoint is a marker that you can set in the source code that tells the browser to pause the execution of the code when it reaches that point. Once execution is paused, you can step through the code, inspect variables, and see the call stack.
5. Source Map: source maps are a feature that allows you to debug the original source code, even when it has been transformed and minified for production.
6. Automatic Error tracking: There are many automatic error tracking tools that make it easy to track down and fix errors in your JavaScript code, for example, services like Rollbar, Bugsnag, Sentry. These tools can automatically log JavaScript exceptions and provide detailed stack traces and diagnostic information, making it easy to track down and fix issues.

These are some of the most common tools and techniques used to debug JavaScript code, depending on the complexity and context of the project, you may use different combination of them to find and fix issues quickly.

### 25. Explain the difference between mutable and immutable objects.

- What is an example of an immutable object in JavaScript?
- What are the pros and cons of immutability?
- How can you achieve immutability in your own code?

In programming, the terms "mutable" and "immutable" refer to whether or not an object's state can be changed after it's created.

- A mutable object is an object whose state can be modified after it's created. For example, a JavaScript array is mutable because you can add, remove, and change elements after it's created.
- An immutable object is an object whose state cannot be modified after it's created. Once an immutable object is created, its state cannot be changed.

In JavaScript, some examples of immutable objects are numbers, strings, and booleans. For example, once a string is created, you can't change a specific character of it, you have to create a new string instead.

The main advantage of immutability is that it helps to ensure that the state of an application remains consistent and predictable. Since the state of an immutable object can't change, it's less prone to errors, and it's easier to reason about and debug.

The main disadvantage of immutability is that it can be less efficient in terms of memory usage, especially in JavaScript where objects are passed by reference. Creating new copies of large data sets can be costly in terms of memory usage and computation time.

To achieve immutability in JavaScript, you have several options:

- Use the **`Object.freeze()`** method to make an object immutable. This method prevents properties from being added, removed, or modified on an object.
- Use the **`Object.assign()`** method to create a new object, with the same properties as an existing object, but with different values.
- Use libraries such as **`immutable.js`**, that provide an implementation of immutable data structures, such as List, Map and Set.

In summary, mutable objects can be modified after they're created, whereas immutable objects can't be. In JavaScript, some examples of immutable objects are numbers, strings, and booleans. Immutable objects are useful in terms of keeping the state of an application consistent, predictable and reduce bugs, but it can come at a cost of performance. You can achieve immutability in JavaScript by using **`Object.freeze()`**, **`Object.assign()`**, or libraries like **`immutable.js`**.

### 26. Explain the difference between synchronous and asynchronous functions.

Okay, imagine you and your friend are playing a game where you take turns to draw a card from a deck of cards. If you take turns one at a time, and you can only pick up one card at a time, that's like a "synchronous" game. But if you and your friend can pick up multiple cards at the same time and put them on a different pile, that's like an "asynchronous" game.

In programming, a synchronous function is a function that runs one step at a time, one after the other, like a line of people. It will wait for the first step to finish before it starts the next step.

An asynchronous function is a function that can run multiple steps at the same time, like many people working on different tasks at the same time. This type of function doesn't have to wait for the first step to finish before it starts the next one.

For example, if you want to make a cake, and you first have to mix the ingredients, then bake it, and then decorate it. If you mix the ingredients, wait for them to be mixed, then bake it and wait for it to be baked and then decorate it, this is a synchronous way of doing it. But if you are able to mix ingredients, then put the cake in the oven and at the same time while the cake is baking, you can start decorating it, this would be asynchronous way of making a cake.

So, asynchronous functions can do multiple things at the same time, while synchronous functions do one thing at a time.

### 27. What is event loop? What is the difference between call stack and task queue?

Okay, imagine you and your friend are playing a game where you each have your own list of things to do, and you are taking turns to do one thing at a time. The list of things that you need to do is like a "call stack" and the list of things your friend needs to do is like a "task queue".

The "event loop" is like a teacher or a leader who is in charge of making sure that everything is done in the right order and making sure that everyone is taking their turns.

The "call stack" is a list of things that the computer is currently working on, it's like a to-do list of things that the computer needs to finish first. Each time the computer needs to do something, it adds it to the top of the list like putting a new task on top of the list.

The "task queue" is like a waiting list of things that the computer needs to do next, it's like a list of things that are waiting to be done. These are tasks that are scheduled to be completed, but the computer has not gotten to them yet.

When the "event loop" is running, it looks at the call stack first and does the top thing on the list. When the top thing is finished, the event loop takes the next thing off the task queue and adds it to the call stack, so the computer can start working on it. This way, the event loop makes sure that everything gets done in the right order, and no task is missed or forgotten.

So, in short, the "event loop" is the mechanism that manages the flow of tasks, the "call stack" is a list of currently executing functions, and the "task queue" is a list of functions waiting to be executed.

### 28. What are the differences between variables created using `let`, `var` or `const`?

When we write computer programs, sometimes we need to store information in a special spot so we can use it later, just like how you put your toys in a toy box. These special spots are called "variables", and JavaScript has different ways of making these variables, like using "let", "var" or "const".

"var" is like a toy box that you can keep opening and putting new toys inside, or taking toys out as many times as you want.

"let" is like a toy box that you can keep opening and putting new toys inside, but you can't take the toys out once they are inside.

"const" is like a toy box that you can put toys inside once, but you can't open it again and put more toys or take any out.

In short, variables created using "var" can be reassigned a new value at any time, variables created using "let" can be reassigned but not redeclared, variables created using "const" can not be reassigned or redeclared.

It's important to choose the right type of toy box depending on what you need to do in your program. If you know you will need to change the value of the variable often, use "var" or "let", if you want the value to remain the same use "const".

### 29. What are the differences between ES6 class and ES5 function constructors?

ES6 introduced a new way to create classes in JavaScript called "class syntax", it is a more simpler and easier way to create objects and their methods.

ES5, on the other hand, uses a function constructor to create objects and their methods.

Here are the main differences between the two:

- Syntax: The syntax for creating classes in ES6 is much simpler and more similar to other object-oriented languages. With ES6 class syntax, you use the **`class`** keyword, followed by the class name, and then the class body inside curly braces.

```jsx
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHello() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

In contrast, in ES5, you create a function constructor and use the **`new`** keyword to create an object.

```jsx
function Person(name) {
  this.name = name;
  this.sayHello = function() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

- **`constructor`** method: In ES6, the **`constructor`** method is used to initialize the object's properties, whereas in ES5, the function constructor itself is used to initialize the object's properties.
- **`prototype`**: In ES5, methods are added to the object's **`prototype`** property, whereas in ES6, methods are defined directly in the class body.

```jsx

// ES5
Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
}

// ES6
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHello() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

In summary, the ES6 class syntax

### 30. Can you offer a use case for the new arrow `=>` function syntax? How does this new syntax differ from other functions?

The new arrow function syntax (also known as "arrow functions") in JavaScript is a shorthand way of writing functions. It uses the "=>" symbol to define a function, rather than the traditional "function" keyword.

The main difference between arrow functions and traditional function syntax is the way they handle the "this" keyword. In traditional function syntax, the value of "this" is determined by how the function is called. In arrow functions, the value of "this" is determined by the context in which the arrow function is defined. This can make arrow functions especially useful in certain situations, such as working with object-oriented programming and closures.

An example of when you would use an arrow function is when you want to use it within an object literal. A common pattern in javascript is to use **`bind`**, **`call`**, **`apply`** to pass the correct **`this`** context to a function, but with arrow function, the **`this`** inside the function refers to the scope in which it is defined, so you don't have to use **`bind`** to pass context.

Here is an example:

```

const obj = {
  name: "John",
  sayName: function() { console.log(this.name) } // traditional function syntax
  sayNameArrow: () => {console.log(this.name)} // arrow function
};
obj.sayName(); // logs "John"
obj.sayNameArrow(); // logs "John"
```

Another example is when you want to use it as a callback function:

```jsx
const numbers = [1, 2, 3, 4];
numbers.forEach(function(number) {
  console.log(number);
});
//the same could be done using arrow function like this:
numbers.forEach(number => console.log(number));
```

In short, the arrow function syntax is a shorthand for writing functions that can make your code shorter and more readable, it uses "=>" symbol instead of the "function" keyword. Its behavior of the **`this`** keyword also different from traditional function, making it useful in certain situations like working with object-oriented programming and closures.

### 31. What advantage is there for using the arrow syntax for a method in a constructor?

Using the arrow function syntax for methods defined within a constructor has a major advantage over using the traditional function syntax, it allows you to correctly bind the value of the **`this`** keyword to the instance of the object, rather than the constructor function or the global context.

In traditional function syntax, the value of **`this`** inside the function depends on how the function is called. When a method defined using traditional function syntax is called on an object, **`this`** refers to the object that the method is being called on. However, when a method defined using traditional function syntax is called on its own, **`this`** refers to the global context or the constructor function, which can cause bugs and unexpected behavior.

However, when you use the arrow function syntax for methods defined within a constructor, the value of **`this`** is determined by the lexical scope, which is the code block that surrounds the arrow function. Since the constructor is the code block that surrounds the arrow function method, **`this`** refers to the current instance of the object, rather than the constructor function or the global context, so you don't have to use **`bind`** to pass context.

Here is an example of how the traditional function syntax would behave and how the arrow function syntax would behave inside a constructor:

```jsx
function Person(name){
  this.name = name;
  this.greet = function(){
    console.log(`Hello, ${this.name}`);
  }
}
const john = new Person("John");
const greet = john.greet;
greet(); // logs "Hello, undefined"

//using arrow function
function Person(name){
  this.name = name;
  this.greet = () => {
    console.log(`Hello, ${this.name}`);
  }
}
const john = new Person("John");
const greet = john.greet;
greet(); // logs "Hello, John"
```

In summary, using arrow function syntax for methods defined within a constructor allows you to correctly bind the value of the **`this`** keyword to the instance of the object, which can prevent bugs and unexpected behavior.

### 32. What is the definition of a higher-order function?

A higher-order function is a special kind of function that can do something extra special. It's like a superhero function! It can either:

- take one or more functions as arguments
- return a new function as its result

Just like how a superhero can do special things that regular people can't, like fly or become invisible, a higher-order function can do special things with functions, like change them or use them in special ways.

Here's an example that could help explain it better: Imagine you have a toy box with many different toy cars inside, and you want to sort them by color. A normal function would only be able to sort them by color one at a time, but a higher-order function is like a special helper that can sort all the cars in the toy box by color at once.

Here's an example in code:

```jsx
function add(x, y) {
  return x + y;
}

function multiply(x, y) {
  return x * y;
}

function operate(operator, x, y) {
  return operator(x, y);
}
console.log(operate(add, 2, 3)); // 5
console.log(operate(multiply, 2, 3)); // 6
```

In the above example, **`operate`** is a higher-order function, because it takes a function as an argument, in this case it takes **`add`** and **`multiply`** as an argument and use them to return the results.

So in short, a higher-order function is a function that can either take one or more functions as arguments or return a new function as its result. It can do special things with functions, like change them or use them in special ways.

### 33. Can you give an example for destructuring an object or an array?

Sure! Here's an example of destructuring an object:

```jsx
let person = { name: "John", age: 30, city: "New York" };
let { name, age } = person;
console.log(name); // "John"
console.log(age); // 30
```

In this example, we have an object called **`person`** with properties **`name`**, **`age`**, and **`city`**. We use the **`let {name, age} = person`** statement to "unpack" the **`name`** and **`age`** properties from the **`person`** object and assign them to new variables with the same name.

Here is an example for destructuring an array:

```jsx
let colors = ['red', 'green', 'blue'];
let [first, second] = colors;
console.log(first); // "red"
console.log(second); // "green"
```

In this example, we have an array called **`colors`** with 3 elements. We use the **`let [first, second] = colors`** statement to "unpack" the first and second elements of the **`colors`** array and assign them to new variables with the same name.

With destructuring, you can extract data from arrays and objects easily and cleanly. It is a powerful feature that allows you to extract properties or elements from objects or arrays, and assign them to variables with a more concise and readable syntax.

### 34. Can you give an example of generating a string with ES6 Template Literals?

In JavaScript, we can use template literals (also known as template strings) to easily create strings that include the values of variables. These strings are defined using backticks (`) instead of quotes (' or ") and can include expressions that are evaluated and included in the final string.

Here is an example of using template literals to generate a string that includes the values of variables:

```jsx
const name = "John";
const age = 30;
const message = `My name is ${name} and I am ${age} years old.`;
console.log(message);
// Output: "My name is John and I am 30 years old."
```

In this example, the template literal includes two expressions: **`${name}`** and **`${age}`**. These expressions are replaced by their corresponding values "John" and "30" when the string is created.

You can also use template literals for multi-line strings, and also doing simple mathematical operations or even function calls inside the expressions.

```
const x = 5, y = 10;
const result = `The sum of ${x} and ${y} is ${x+y}`;
console.log(result);
// Output: "The sum of 5 and 10 is 15"
```

### 37. Can you give an example of a curry function and why this syntax offers an advantage?

Sure! Here's an example of a curry function in JavaScript:

```jsx
const curry = (fn) => {
  return (...args) => {
    if (args.length >= fn.length) {
      return fn(...args);
    }
    return curry(fn.bind(null, ...args));
  };
}

const add = curry((x, y) => x + y);
const add5 = add(5);
console.log(add5(3)); // 8
console.log(add5(10)); // 15
```

In this example, we have a **`curry`** function that takes a function **`fn`** as an argument. The **`curry`** function returns a new function that takes any number of arguments (using the **`...args`** rest operator).

The inner function first checks if the number of arguments passed to it is equal or greater than the number of arguments expected by the original function, **`fn`**. If it is, it calls **`fn`** with the passed arguments. If not, it returns a new function that is bound to the previous arguments, and this new function can be invoked with the remaining arguments to eventually invoke the original function **`fn`** with all the arguments.

When we call **`const add5 = add(5)`** the **`add(5)`** invokes the returned function from **`curry`** and pass 5 as an argument, the inner function returns a new function that already has 5 as its first argument. This new function **`add5`** is now invoked with the remaining arguments and it returns the expected result.

Curry functions allow us to create a new function that is already partially applied with some of the arguments, and this offers an advantage by allowing us to create reusable, composable, and more readable code.
It also allows us to create functions with a more functional approach, where we can create more specialized functions by partially applying some of the arguments before calling the main function.

### 38. What are the benefits of using `spread syntax` and how is it different from `rest syntax`?

Spread and Rest syntax are both ways to work with multiple items at once, but they are used in different ways.

Spread syntax is like taking a big bag of things and spreading them out, so you can see all of them. It allows you to take an array or an object, and spread its items out into multiple elements. For example, you can use spread syntax to add multiple items to an array at once:

```jsx
let fruits = ["banana", "apple"];
let newFruits = ["orange", "mango", ...fruits];
console.log(newFruits); // ["orange", "mango", "banana", "apple"]
```

Rest syntax is like taking a big bag of things and gathering them together, so you can carry them in one hand. It allows you to take multiple items and gather them together into an array or an object. For example, you can use rest syntax to gather multiple items into an array:

```jsx
function sum(...args) {
  return args.reduce((acc, value) => acc + value, 0);
}
console.log(sum(1, 2, 3, 4));  // 10
```

In short, Spread syntax is like spreading things out, so you can see all of them, it allows you to take an array or an object and spread its items out into multiple elements. Rest syntax is like gathering things together, so you can carry them in one hand, it allows you to take multiple items and gather them together into an array or an object.

### 39. How can you share code between files?

There are several ways to share code between files in JavaScript:

1. **Exporting and Importing Modules**: JavaScript has built-in support for modules, which allows you to export variables, functions, or objects from one file and import them into another file.

```jsx
// file1.js
export const myFunction = () => {...};
export const myVariable = "Hello";

// file2.js
import { myFunction, myVariable } from "./file1.js";
```

2. **ES6 `export default` and `import`**: You can also use the **`export default`** syntax to export a single value from a file, and use the **`import`** statement to import it into another file.

```jsx
// file1.js
const myFunction = () => {...};
export default myFunction;

// file2.js
import myFunction from "./file1.js";
```

3. **CommonJS `module.exports` and `require`**: CommonJS is a module system that is used in environments like Node.js. In CommonJS, you use the **`module.exports`** object to export values from a file, and the **`require`** function to import them into another file.

```jsx
// file1.js
const myFunction = () => {...};
module.exports = myFunction;

// file2.js
const myFunction = require("./file1.js");
```

4. **Using script tags**: You can also include JavaScript files in an HTML document using the **`<script>`** tag, and the code in those files will be available to the whole document.

```jsx
<script src="file1.js"></script>
<script src="file2.js"></script>
```

These are the main ways to share code between files, and the choice of which one to use depends on the specific use case and the environment where the code is running.

It's worth noting that the last method is not recommended as it can cause issues with code order and it's not as flexible and maintainable as the other methods.

### 40. Why you might want to create static class members?

A static class member is a property or a method that belongs to a class itself, and not to any object created from that class.

Imagine you have a class called "Teacher" and you want to store the number of teachers in your school. You can create a static variable called "numberOfTeachers" and increment it every time you create a new teacher.

```jsx
class Teacher{
    static numberOfTeachers = 0;
    constructor(name){
        this.name = name;
        Teacher.numberOfTeachers++;
    }
}
const teacher1 = new Teacher("Ms. Smith");
const teacher2 = new Teacher("Mr. Johnson");
console.log(Teacher.numberOfTeachers); // 2
```

This way you can count how many teachers are in your school without creating an instance of the teacher class or keeping track of each teacher object you create.

Another example is when you want to create a method that does not depend on any object's state, for example, a method that convert from Celsius to Fahrenheit, you don't need to know the current temperature to perform this conversion.

```
class Temperature {
    static celsiusToFahrenheit(celsius) {
        return celsius * 9/5 + 32;
    }
}
console.log(Temperature.celsiusToFahrenheit(20)); // 68
```

In this example, the static method **`celsiusToFahrenheit`** is shared by all instances of the class and it's available even if you don't create an instance of the class.

So, creating static class members is useful when you want to store information or methods that don't depend on the state of an object created from that class, it's a way to share some behavior or data across all instances of the class and make it available without creating an object.

### 41. What is the difference between `while` and `do-while` loops in JavaScript?

In JavaScript, both **`while`** and **`do-while`** loops are used to repeatedly execute a block of code, but they differ in when the code block is executed.

A **`while`** loop checks the condition before executing the code block. If the condition is true, the code block will be executed, and then the condition will be checked again. This process continues until the condition is false.

```jsx
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

A **`do-while`** loop, on the other hand, executes the code block first, and then checks the condition. If the condition is true, the code block will be executed again, and the process repeats until the condition is false.

```jsx
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

In short, the difference between a **`while`** loop and a **`do-while`** loop is that a **`while`** loop checks the condition before executing the code block and a **`do-while`** loop executes the code block first and then checks the condition.

### 42. What is a promise? Where and how would you use promise?

A promise is like a gift that you give to someone, it's something that you promise to do or give them in the future. In JavaScript, a promise is an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

For example, imagine you promise your friend to give them a toy, they will get the toy at some point in the future. Your friend can choose to wait for the toy or do something else.

In the same way, when you use a promise in JavaScript, you are telling the computer to do something and it will give you the result at some point in the future, and you can choose to wait for the result or do something else.

Promises are commonly used for handling asynchronous operations such as fetching data from a server, reading files, or performing animations. For example, you could use a promise to fetch data from a server like this:

```jsx
fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
  .then(json => console.log(json))
  .catch(error => console.log(error));
```

In short, A promise is like a gift that you give to someone, in JavaScript, it's an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value. Promises are commonly used for handling asynchronous operations such as fetching data from a server, reading files, or performing animations.

### 43. Discuss how you might use Object Oriented Programming principles when coding with JavaScript.****

JavaScript is a multi-paradigm programming language, meaning it supports different programming styles, including object-oriented programming (OOP). OOP is a programming paradigm that uses objects, classes and their interactions to design applications and computer programs.

In JavaScript, OOP is implemented using objects, constructors, and prototypes. Here are a few ways to apply OOP principles when coding with JavaScript:

- Objects: JavaScript objects are used to store data and methods. They can be created using the object literal notation or the object constructor. You can use objects to model real-world entities such as a car, person, or bank account.
- Constructors: JavaScript constructors are used to create objects with a specific structure and behavior. They are defined using the **`function`** keyword and are invoked using the **`new`** keyword. Constructors can be used to create multiple objects with similar properties and methods.
- Prototypes: JavaScript prototypes are used to create object inheritance. Every object in JavaScript has a prototype object, which is used to inherit properties and methods. You can use prototypes to create a parent-child relationship between objects and reuse common properties and methods across multiple objects.
- Classes: Classes are introduced in ECMAScript 6, and allow to create objects with a specific structure and behavior. They are defined using the **`class`** keyword and can be used to create multiple objects with similar properties and methods.
- Encapsulation: It's the practice of keeping the internal state of an object private and providing a public interface for interacting with it. You can use closures to encapsulate the internal state of an object in JavaScript.
- Abstraction: It's the practice of hiding the implementation details of an object and exposing only the necessary information. You can use interfaces, abstract classes or class inheritance to achieve abstraction in JavaScript.

In short, Object-Oriented Programming principles can be applied to JavaScript by using objects, constructors, prototypes, classes, encapsulation and abstraction. These concepts

### 44. What is the difference between e.target and e.currentTarget?

In JavaScript, the **`e.target`** and **`e.currentTarget`** properties are used to access the element that triggered an event and the element that the event listener is attached to, respectively.

- **`e.target`**: It refers to the element that actually triggered the event, it can be a child of the element that the event listener is attached to.
- **`e.currentTarget`**: It refers to the element that the event listener is attached to, it is the element that you attached the event listener to.

For example, consider the following HTML structure:

```jsx
<div id="parent">
  <button id="child">Click me</button>
</div>
```

In this example, if you attach an event listener to the parent div and you click on the button, the **`e.target`** will be the button and the **`e.currentTarget`** will be the parent div.

In short, **`e.target`** refers to the element that actually triggered the event, and **`e.currentTarget`** refers to the element that the event listener is attached to.

### 45. Is there any difference between Promises and callbacks? Which is better?

Promises and callbacks are both ways to handle asynchronous operations in JavaScript, but they work differently.

Callbacks are functions that are passed as arguments to other functions and are called when the operation they are associated with completes. They are widely used in JavaScript, and are supported by most JavaScript APIs.

Promises, on the other hand, are a more modern way of handling asynchronous operations. They are objects that represent the eventual completion or failure of an asynchronous operation and its resulting value. Promises provide a consistent way of handling async operations, by using the **`then`** and **`catch`** methods. They also have a few additional features such as chaining and error handling.

Both callbacks and Promises can be used to handle asynchronous operations, but Promises have some advantages over callbacks, such as:

- Promises make it easier to handle errors and to chain async operations, by using the **`catch`** method, instead of having to pass an error-handling callback as an argument.
- Promises make it easier to reason about async code, as they have a clear and consistent API, and they make the code look more synchronous.
- Promises make it easier to deal with async operations that return multiple values, by allowing you to return multiple values through multiple **`then`** callbacks.
- Promises make it easier to deal with async operations that need to be cancelled, by providing an easy way to cancel the ongoing operation.

In short, Promises and callbacks are both ways to handle async operations, but Promises provide a more consistent and modern way to handle async operations, making the code look more synchronous, making it easier to reason about async code, easier to handle errors, and providing an easy way to cancel the ongoing operation.

### 46. What is recursion? When is the use of recursion useful in Javascript?

Recursion is a technique in computer science where a function calls itself in order to solve a problem. A function that calls itself is called a recursive function.

Recursion can be useful in JavaScript when the problem can be divided into smaller, similar sub-problems. These sub-problems are solved using the same function, which is called recursively until the base case is reached. The base case is the point at which the recursion stops.

For example, consider a problem of finding the factorial of a number. Factorial is the product of an integer and all the integers below it, for example, 5! = 5*4*3*2*1 = 120. This problem can be solved using recursion by breaking it down into smaller sub-problems, such as finding the factorial of n-1, where n is the input number.

```jsx
function factorial(n) {
    if (n === 0) {
        return 1;
    }
    return n * factorial(n-1);
}
console.log(factorial(5)); //120
```

Another example is traversing a tree-like data structure, such as a file system, where recursion can be used to traverse through all the files and directories.

In short, recursion is a technique in computer science where a function calls itself to solve a problem, it is useful when the problem can be divided into smaller, similar sub-problems, it uses a base case to stop the recursion and it's useful in Javascript in situations like finding the factorial of a number, traversing a tree-like data structure, etc.

### 47. What do you hear about DRY, KISS, YAGNI?

DRY, KISS, and YAGNI are software development principles that help developers write better code.

- DRY stands for "Don't Repeat Yourself". It's a principle that states that you should avoid duplicating code, and instead, you should use abstraction, encapsulation, and inheritance to share common functionality. DRY code is more maintainable, and easier to update, debug and test.
- KISS stands for "Keep It Simple, Stupid". It's a principle that states that you should keep your code simple and easy to understand. Simple code is more readable, more maintainable, and less prone to bugs.
- YAGNI stands for "You Ain't Gonna Need It". It's a principle that states that you should only write code that is immediately necessary to meet the requirements of the current task. YAGNI promotes writing code that is focused, and avoids unnecessary complexity, bloat, and technical debt.

These principles are closely related, and they help developers to write more maintainable, more scalable and easier to understand code. They are also important to help developers to make the right decisions when it comes to choosing the tools, technologies, and design patterns to use.

### 48. What do you know about optional chaining operators? What benefits does it bring?

Optional chaining operators are a new feature introduced in ECMAScript 2020, that allows you to access properties of an object without having to check if the object or any of its parent objects are undefined or null. It makes it easier to access deeply nested properties, without having to check for the existence of each object along the way.

The optional chaining operator is represented by the "?." symbol, it can be used to access properties of an object, even if the object or any of its parent objects are undefined or null. If any of the objects in the chain are undefined or null, the expression will return undefined instead of throwing an error.

```
let user = {
  name: "John",
  age: 25,
  address: {
    street: "Main St",
    city: "New York"
  }
};
console.log(user?.address?.city); // "New York"
console.log(user?.phone?.number); // undefined
```

The Optional chaining operator can also be used to call functions and methods, even if the object or any of its parent objects are undefined or null. If any of the objects in the chain are undefined or null, the expression will return undefined instead of throwing an error.

```jsx
let user = {
  name: "John",
  age: 25,
  address: {
    street: "Main St",
    city: "New York"
  },
  getFullAddress: function(){
    return this.address.street + ", " + this.address.city;
  }
};
console.log(user?.getFullAddress()); // "Main St, New York"
```

### 49. What patterns do you know and successfully use in JavaScript?

There are several design patterns that are commonly used in JavaScript:

- The Module pattern: This pattern is used to encapsulate data and methods, creating a public and private interface, and it's often used to create objects that act as namespaces, this is done by creating an object and returning an object containing the public methods.
- The Factory pattern: This pattern is used to create objects without specifying the exact class of object that will be created, it allows objects to be created based on certain criteria.
- The Singleton pattern: This pattern is used to ensure that only one instance of a class is created, it also provides a global point of access to the object.
- The Observer pattern: This pattern is used to create a one-to-many dependency relationship between objects, so that when one object changes its state, all its dependents are notified.
- The Decorator pattern: This pattern is used to add new functionality to an existing object, without affecting the behavior of other objects from the same class.
- The Prototype pattern: This pattern is used to create new objects by cloning existing objects, it is a way to create an instance of an object without specifying the exact class of object that will be created.
- The Command pattern: This pattern is used to encapsulate a request as an object, which allows the request to be treated as an object, it decouples the sender and the receiver of a request.

These are some of the most common patterns used in JavaScript, they are designed to help developers to write more maintainable, scalable, and easy to understand code. They also help to make the right decisions when choosing the tools, technologies, and design patterns to use.

### 50. What is SOLID?

SOLID is an acronym that stands for five design principles for object-oriented programming and class design:

- Single Responsibility Principle (SRP): A class should have only one reason to change, meaning that a class should have only one responsibility, and that all its methods should be related to that responsibility.
- Open-Closed Principle (OCP): A class should be open for extension but closed for modification, meaning that a class should be designed in such a way that new functionality can be added to it without modifying the existing code.
- Liskov Substitution Principle (LSP): Subtypes should be substitutable for their base types, meaning that objects of a superclass should be able to be replaced with objects of a subclass without affecting the correctness of the program.
- Interface Segregation Principle (ISP): A class should not be forced to implement interfaces it does not use, meaning that a class should only be required to implement the methods that it needs to use.
- Dependency Inversion Principle (DIP): High-level modules should not depend on low-level modules, but they should depend on abstractions, meaning that the design should aim to reduce the dependencies between modules and increase the use of interfaces and abstract classes to decouple the code.

The SOLID principles are a set of guidelines that help developers to create more maintainable, scalable, and easy to understand code. These principles encourage developers to write code that is more flexible, less prone to bugs, and easier to extend and maintain over time.
