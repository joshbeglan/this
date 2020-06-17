# The JavaScript this Keyword

## What is this?

The JavaScript `this` keyword refers to the object it belongs to. 

**`this` has different values depending on where it is used:**

* Alone, `this` refers to the global object.
* In a method, `this` refers to the owner object.
* In a function, `this` refers to the global object.
* In a function, in strict mode, `this` is undefined.
* In an event, `this` refers to the element that received the event.
 
#### `this` Alone

When used alone, this refers to the global object.

In a browser window the global object is the `window` object:

**Example (copy and paste this code into your console)**
```js 
var x = this;
console.log(x); //prints the global window object
```
 

#### `this` in a Method

Before now, we have been using the term method and function interchangeably, but there is a slight difference. A method is a function that you invoke **off of an object**. For example, `fullName()` is an example of calling a function, but `person.fullName()` is an example of calling a method. Because we type "person DOT fullname", we are invoking the fullName method off of the person object. Another explanation is that the person object **owns** the fullName method. 

In a method, `this` refers to the "owner" of the method.

**Example (copy and paste this code into your console)**
```js
var person = {
  firstName: "John",
  lastName : "Doe",
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};
person.fullName(); //returns the string "John Doe" 
```
 
In the example above, `this` refers to the person object.
The person object is the owner of the fullName method. In other words: **this.firstName** means the **firstName** property of **this** (person) object.




### `this` in a Function (Default)

In a JavaScript function, this refers to the global object `window`.

**Example (copy and paste this code into your console)**
```js
function myFunction() {
  return this;
}
myFunction(); //returns the global window object
```
 
### `this` in a Function (Strict)

JavaScript strict mode does not allow default binding.
So, when used in a function, in strict mode, `this` is undefined.

**Example (copy and paste this code into your console)**
```js
"use strict";
function myFunction() {
  return this;
}
myFunction(); //returns undefined
```
 

### `this` in Event Handlers

In HTML event handlers, `this` refers to the HTML element that received the event:

**Example (copy and paste this code into your console)**
```js
document.body.addEventListener("click", handleClick)
function handleClick(e){
	console.log(this)
}
//clicking anywhere in the DOM will console log the body element
```

### Explicit Function Binding

`bind()` is a predefined JavaScript method.

This `bind()` method is called off a function object and **returns a new function** where the value of `this` is binded (a predetermined value)

In the example below, when calling `printFullName.bind` with person as the argument, it will return a new function where the value of `this` is the person object. 

**Example (copy and paste this code into your console)**
``js
var person = {
  firstName: "John",
lastName: "Doe" 
}

function printFullName() {
	console.log(this.firstName + " " + this.lastName)
}

printFullName() //console logs "undefined undefined"

var func = printFullName.bind(person);  // Will return a new function which we save as func

func() //console logs "John Doe"
``
 
When we invoke `printFullName()`, the value of `this` in a function is the `window` object, and since `window` does not have a firstName or lastName property, we get `"undefined undefined"`.  `printFullName.bind(person)` returns a new function object which we store in a variable called `func`. When we invoke `func()`, the value of `this` is no longer the `window` object, but instead, the value of `this` has been **binded** to the person object.          
