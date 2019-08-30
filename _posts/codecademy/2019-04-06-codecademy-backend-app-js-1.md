---
layout: post
title: "Codecademy - Back-End App with JavaScript 1"
categories: [web]
tags: [javascript, codecademy web, codecademy, codecademy js]
toc: 1
comment: 1
---

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
