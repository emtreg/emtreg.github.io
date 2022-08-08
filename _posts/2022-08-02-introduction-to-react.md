---
layout: post
title: "Introduction to React"
date: 2022-08-02
---

<p>&emsp;react.js is a JavaScript library used for building user interfaces. React is fast, modular, scalable and flexible.</p>

<!--more-->

<p><strong>JSX</strong></p>

<p>&emsp;It utilizes JSX, which is a syntax extension for JavaScript that looks like HTML. A <em>JSX compiler</em> is needed so browsers can read the code from a JS file. </p>

<p>&emsp;Example of a JSX element in JavaScript:</p>

```javascript
const h1 = <h1>Hello World</h1>;
```

<p>&emsp;JSX elements are treated like JS expressions. They can be saved in a variable, passed to a function, or stored in an object or array. They can also have attributes and can be nested within other JSX elements.</p>

<p>&emsp;For example, the above JSX element could also have a style attribute: </p>

```javascript
const h1 = <h1 style="color:red;">Hello World</h1>;
```

<p>&emsp;Or could be nested:</p>

```javascript
const h1 = <a href="https://www.example.com"><h1 style="color:red;">Hello World</h1></a>;
```

<p>&emsp;If a JSX expression takes up more than one line it needs to be wrapped in parenthesis. The above could also be written as: </p>

```javascript
const h1 = (
   <a href="https://www.example.com">
     <h1>
       Hello World
     </h1>
   </a>
 );
```
<p>&emsp;A JSX expression must have exactly one outermost element. The below code is invalid: </p>

```javascript
const expression = (
   <p>Text<p>
   <p>More text</p>
 );
```
<p>&emsp;You can instead wrap the expression in div tags: </p>

```javascript
const expression = (
   <div>
      <p>Text<p>
      <p>More text</p>
   </div>
 );
```
