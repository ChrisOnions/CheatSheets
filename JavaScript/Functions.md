# Types of Functions

## Function Declarations

```Javascript
// Declare the Function
function square(number) {
  return number * number;
}
// Call the Function
square(2)
```

# Scope and the Function stack

## Recursive Function

Recursion
A function can refer to and call itself. There are three ways for a function to refer to itself:

- The function's name
- arguments.callee
- An in-scope variable that refers to the function

```Javascript
// Assign the function to a variable
let square_func = function square() {
   return number * number;
}
// Basic syntax
function validFunctionName(parameter) {
  return statement;
  }
```

# Arrow Functions

- Aka : Fat Arrows

```Javascript
// Minimal Syntax
() => {}

// Arrow Function
const double = (value) => {
  return value * 2
}

double(10);
// Output : 20

// You dont need return on simple opperations
const double2 = value => value * 2;
```

# Higher order Functions

```Javascript
// Add here
```

# Callbacks

```Javascript
// Add here
```

# Factory Functions

A factory function is any function which is not a class or constructor that returns a (presumably new) object. In JavaScript, any function can return an object. When it does so without the new keyword, it’s a factory function.

```Javascript
//
const user = {
  userName: 'echo',
  avatar: 'echo.png'
};
console.log(user.userName);

//
const userName = 'echo';
const avatar = 'echo.png';
const user = {
  userName,
  avatar,
  setUserName (userName) {
    this.userName = userName;
    return this;
  }
};
console.log(user.setUserName('Foo').userName);
```

[Read More - W/Destructuring](https://medium.com/javascript-scene/javascript-factory-functions-with-es6-4d224591a8b1)

# Generator Functions

The function\* declaration (function keyword followed by an asterisk) defines a generator function, which returns a Generator object.

- Generators in JavaScript -- especially when combined with Promises -- are a very powerful tool for asynchronous programming

```Javascript
// Addhere
```

[MDN - Generator Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*)

---
