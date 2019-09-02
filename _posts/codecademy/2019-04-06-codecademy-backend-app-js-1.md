---
layout: post
title: "Codecademy - Back-End App with JS 1"
categories: [web]
tags: [javascript, codecademy web, codecademy, codecademy js]
toc: 1
comment: 1
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
} else{
  // commands
}
~~~

- Comparison Operators: `<, ===, >, >=, <=, !==` 
- Logical operators: `&&, ||, !`

### Functions

### Scope

### Developing JavaScript Apps Locally

## JavaScript Arrays, Loops, and Iterators


## JavaScript Objects, Modules, and Browser Compatibility

## Building Back-End Servers with Express.js

## SQL for Back-End Development


## Connecting JavaScript and SQL


## Back-End Development Capstones

