---
layout: post
title: "Codecademy - Back-End App with JS 1"
categories: [web]
tags: [javascript, codecademy web, codecademy, codecademy js]
toc: 1
comment: 1
date: 2019-09-10
---

{% assign img-url = '/images/posts/codecademy/backend-app-js' %}

This note is created when I started to learn the [Create a Back-End App with JavaScript](https://www.codecademy.com/learn/paths/create-a-back-end-app-with-javascript).

## Tự động thay đổi khi file js thay đổi

- Using [live-server](https://github.com/tapio/live-server)
- Install [nodejs](https://nodejs.org/en/download/) first.
- Install live-server using nodejs: `npm install -g live-server`
- `cd` to the project folder
- run `live-server` (accept all networks notification)
- [http://127.0.0.1:8080/](http://127.0.0.1:8080/)
- Enjoy!

## Miscellaneous

- End of each line: `;`
- Comment: `//`
- Multiline comment: `/* */`
- Print ra console: `console.log("nhung thu can hien ra")`

## JS fundamental

### Console

- a panel that displays important messages
- <kbd>F12</kbd> in Chrome to open console (choose tab **colsole** after that)
- <mark>Trong đây mỗi lần mình `.` là nó gợi ý mấy câu lệnh/thuộc tính hay lắm</mark>
- Thử test vài thứ với `console.log` hoặc `console(15)` hoặc `2+2` hoặc

  ~~~ js
  console.log('Location of Codecademy headquarters: 575 Broadway, New York City');
  ~~~

- **Data Types**: number, string (`'...'` or `"..."`), boolean (`true`, `false`), null (`null`), Undefined (`undefined`), 
- **Làm toán**: `console.log(2+3)`, các phép toán khác: `+,-,*,/,%`
- **String concatenation**: `console.log('hi'+'thi')` produces `'hithi'`
- **Properties**: `console.log('Hello'.length)`
- **Methods**: `.toUpperCase()`, `.startsWith('H')` (check if a string starts with "H"), `.trim()` (removes white spaces)
- **Built-in Objects**: `Math` (perform more complex math operations, [more](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)), `Number` ([ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number))

### Variables

- **Create a variable**: `var <name> = <value>` hoặc dùng `let` thay cho `var` hoặc dùng `const` (thay cho từ *constant*, var định nghĩa bằng cái này **không thể re-assign** + phải có giá trị)
  - Có thể declare mà **không cần value** với `var` hoặc `let`. <-- output: `undefined`
- Difference between `var` and `let`[[ref]](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var):
  - `var`: function scope (có tác dụng trong toàn function)
  - `let`: block scope (có tác dụng trong 1 block nào đó, trong `{}` nào đó)
  - The reason why `let` keyword was introduced to the language was function scope is confusing and was one of the main source of bug in javascript.

    ~~~ js
    var a=1;
    var a=2; // ok, a=2 now
    a=5; // a=5 now
    
    let c=1;
    let c=2; // error
    c=3; // c=3 now
    
    const b=1;
    const b=2; // error
    b=2 // error
    ~~~

- **Mathematical Assignment Operators**: `a +=`, `-=`, `*=`, `/=`.
- **The Increment and Decrement Operator**: `a++` (`a` lấy giá trị mới như `a+1`). `--`.
- `"I'm" + "Thi"`
- Thay thế string có 2 cách:

  ~~~ js
  myName = "Thi"
  console.log("I'm " + myName + ".");
  console.log(`I'm ${myName}.`);
  ~~~

- Check the type of some variable: `typeof <var>`

### JavaScript Versions: ES6 and Before

- JavaScript was introduced in **1995** by **Netscape Communications** as a scripting language for web designers and programmers to interact with web pages. 
- 1996, Netscape submitted JavaScript to a standards developing organization called Ecma International to create **standards for a scripting language** (a type of programming language)
- 1997, Ecma International released **ECMA-262** which sets standards for the first version of a scripting language called **ECMAScript**, shortened to **ES**.
  - provided *rules for the architecture* of JavaScript features
-  when you see **ES6** or **JavaScript ES6**, it means that that version of JavaScript is following the specifications in the <mark>sixth edition of ECMAScript</mark>!
-  ES6 = ES2015

![JS timeline]({{img-url}}/javascript_timeline.svg){:.no-border .w-700}

- ES6 have a big update for ECMAScript
  - new keywords like `let` and `const` to declare variables,
  - new function syntax using Arrow functions,
  - creation of Classes,
  - parameters with default values,
  - promises for asynchronous actions,
  - and many more!

- Compare:

  ~~~ js
  // pre-ES6
  var greeting = function() {
    console.log('Hello World!');  
  };
  
  // ES6
  const greeting = () => console.log('Hello World'); 
  ~~~

## JavaScript Conditionals and Functions

### Conditional Statements

~~~ js
// only if
if (true){
  // commands
}

// if...else
if (true){
  // commands
} else if (true){
  // commands
} else{
  // commands
}

// switch
let var = 'papaya';
switch (var) {
  case 'val1':
    // commands
    break;
  case 'val2':
    // commands
    break;
  case 'val3':
    // commands
    break;
  default:
    // commands
    break;
}
~~~

- Comparison Operators: `<, ===, >, >=, <=, !==` 
- Logical operators: `&&, ||, !`
- short-circuit evaluation: `let defaultName = username || 'Stranger';`
- Ternary Operator: `isNightTime ? console.log('Yes!') : console.log('No!');`

### Functions

~~~ js
function <func>(<parameters>){
  // commands
  // return <var>;
}

// call the function
<func>();

// default parameters
function greeting (name = 'stranger') {
  console.log(`Hello, ${name}!`)
}
~~~

Function Expressions:

~~~ js
const CalculateArea = function(width, height){
  const area = width * height;
  return area;
};
~~~

Arrow Functions (no need to use `function`):

~~~ js
const rectangleArea = (width, height) => {
  let area = width * height;
  return area;
};

// if there is no parameter
const <func> = () => {};

// if there is only one parameter
const <func> = <para> => {};

// single line: no need "{}"
const sumNumbers = number => number + number;
~~~

## Developing JavaScript Apps Locally

### NodeJS

- [Download and install](https://nodejs.org/en/download/) NodeJS.
- Check if node is installed and its version: `node --version`.
- Open terminal, type `node`. Open **Console** giống trên browser!
- <kbd>Ctrl</kbd> + <kbd>C</kbd> 2 times to exit!

### Introduction to Testing with Mocha and Chai

- **What is Unit Testing?**
  - Unit testing means testing the behavior of code in small, independent units.
- **[Mocha](https://mochajs.org/)** and **[Chai](https://www.chaijs.com/)**, Test Suites and Test Cases
  - Mocha and Chai are two JavaScript frameworks commonly used together for unit testing.
- Regular use of keywords: `describe` and `it` in Mocha.
- **Assertions**: 
  - Assertions are tied to particular values (whereas test cases are descriptions of behavior) and they will *fail if the expected value does not match the actual value*.
  - Every assertion in a test case **must be met in order** for the test case to pass.
- **Chai** is an *assertion library* that is often used alongside Mocha, it provides *functions and methods* that help you **compare** the output of a certain test with its expected value. 
  - Exp: `expect(exampleArray).to.have.lengthOf(3);`
- An example test,

    ~~~ js
    describe('setPlayerMoves() - Main Functionality', function() { // this is a `describe` block, everything within this callback function is one test suite
      afterEach(clearMoves); // this is a `hook` that gets called between `it` blocks to reset the state
    
      it('a function called setPlayerMoves should exist', function() { // this is an `it` block, everything inside this function is a single test case
        should.equal(typeof setPlayerMoves, 'function'); // tests often start by checking that the right things exist and are of the right type
      });
    
      it('should set player one\'s moves with valid inputs', function() {
        setPlayerMoves('Player One', 'rock', 11); // here we call a function from the code we are testing that sets play one's move to rock with a value of 11
    
        should.equal(playerOneMoveOneType, 'rock'); // this is an assertion that tests that after the `setPlayerMoves()` function above is called, playerOneMoveOneType should equal `rock`
        should.equal(playerOneMoveOneValue, 11); // this assertion tests that setPlayerMoves can set the value of playerOneMoveOneValue
      });
    })
    ~~~

- Running Tests and Interpreting Output with Mocha and Chai
  - `cd` to project folder.
  - Run `npm install` all necessary testing dependencies.
  - Run `npm test`
  - I’m overwhelmed by the output!: [[ref](https://mochajs.org/#mochaopts)] try appending `.only()` or `.skip()` to your `describe` or `it` blocks to only run certain tests or skip other certain tests.

- **Projects** (see on Github): `project-0-content-creators`, `project-1-rock-paper-scissors-x99`.

### HTTP Requests

- **HTTP** is the command language that the devices on both sides of the connection must follow in order to communicate.
- Type `codecademy.com`, commanding it to open a **TCP** channel to the server that responds to that URL.
- Your computer is **client** (makes the request). The URL is the **server**.
- Once the **TCP connection is established**, client sends `HTTP GET` to retrieve the webpage
- After server has sent the response, it **closes the TCP connection**.

### REST

- [REST](https://en.wikipedia.org/wiki/Representational_state_transfer), is an **architectural style** for providing **standards** between computer **systems on the web**, making it easier for systems to communicate with each other.
- In the REST architectural style, the implementation of the client and the **implementation of the server can be done independently** without each knowing about the other.
- **Statelessness** = server does not need to know anything about what state the client is in and vice versa.