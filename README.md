**Table of Contents**
- [Refactoring Principles](#refactoring-principles)
  - [Separation of Concerns Example](#separation-of-concerns-example)
  - [Abstraction Example](#abstraction-example)
- [TODOs](#todos)
  - [TODO 1) Create your file structure](#todo-1-create-your-file-structure)
  - [TODO 2) Refactor the file structure](#todo-2-refactor-the-file-structure)
  - [TODO 3) Refactor index.js comment headers](#todo-3-refactor-indexjs-comment-headers)
  - [TODO 4) Refactor update](#todo-4-refactor-update)
  - [TODO 5) Refactor handleBoxClick](#todo-5-refactor-handleboxclick)
  - [TODO 6) Reflection](#todo-6-reflection)


# Refactoring Principles

This project will focus on "refactoring" an old project: Bouncing Box.

Refactoring is the process of internally restructuring existing code without changing its external behavior

This project will focus on refactoring for 2 purposes: Separation of Concerns and Abstraction.

### Separation of Concerns Example

The main principle of separation of concerns is: Every file/module/function should perform one task and one task only.

Often, files/functions/modules serve to execute multiple sub-tasks. Consider the following function:

```js
// core logic
function greet() {
  var name = prompt("what is your name?");
  console.log("hello " + name);
  console.log("goodbye " + name);
} 
```

Notice how the `greet` function has 3 distinct sub-tasks that it performs: 
1. asking for a name
2. saying hello with the name
3. saying goodbye with the name

To achieve separation of concerns with this `greet` function, the _implementation_ for each sub-task (the code for _how_ to actually perform a task) should be isolated from one another. 

Below is an example of how it may be refactored:

```js
// core logic
function greet() {
  // ask for name
  var name = getStrangersName();

  // say hello
  sayHello(name);  
  
  // say goodbye
  sayGoodbye(name);
}

// helper functions
function getStrangersName() {
  return prompt("what is your name?");
}

function sayHello(name) {
  console.log("hello " + name);
}

function sayGoodbye(name) {
  console.log("goodbye " + name);
}
```

Notice now that the `greet` function simply invokes/calls the other three functions. It's main purpose is to tie together the other functions while the other functions can focus on performing their one task.

In addition, comments have been added to clarify the purpose of each subtask and to organize the `core logic` from the `helper functions`.

### Abstraction Example

Abstraction is the process of turning something specific (hard-coded) into something generic (reusable)

Repetitive code presents an opportunity to refactor for abstraction. Abstraction helps us to follow the D.R.Y. principle (don't repeat yourself).

To refactor repetitive code for abstraction, you can follow these 3 steps:
1. identify the repetetive statements and turn those statements into a new function declaration
2. identify the changing expressions/data (if any) and turn those expressions/data into parameters
3. replace repetitive code with function calls

Below is an example of refactoring for abstraction. Consider the following code which rolls dice of different sizes:

```js
var roll1 = Math.ceil(Math.random() * 6);
var roll2 = Math.ceil(Math.random() * 10);
var roll3 = Math.ceil(Math.random() * 20);
```

Notice that each time I roll the dice I am using the `Math.ceil()` and `Math.random()` functions, the `*` operator and a number value. These statements can be turned into a new function declaration.

However, the number value changes each time so that value must be replaced with a parameter.

Below is how this code may be refactored for abstraction:

```js
function rollDice(sides) {
  return Math.ceil(Math.random() * sides);
}

var roll1 = rollDice(6);
var roll2 = rollDice(10);
var roll3 = rollDice(20);
```

# TODOs

### _Remember to use `control+c` and `control+v` to copy and paste_

## TODO 1) Create your file structure
- Sign into / open your IDE of choice (cloud9, VS Code, sublime, etc...)
- Create a new folder with the name: `bouncing-box-refactor`
- Create 3 files in that folder: `index.html`, `index.css`, `index.js`
- Copy the code from bouncing box jsbin (see below) into `index.html`

[Bouncing Box jsbin: Right Click --> Open Link in New Tab](https://jsbin.com/goyuhod/edit?html,output)

## TODO 2) Refactor the file structure

#### Step 1: Use your google search powers to figure out how to:
1. `add an external css file to an html file`
2. `add a javascript file to an html file`

Hint: include "w3schools" in your search query

#### Step 2: move the CSS:
- Copy and paste the CSS within the `<style>` tags from `index.html` to `index.css`
- Link the index.css file to the `index.html`file within the `<head>` tags

Hint: the code you are copy-pasting should look like the code below:

```css
.box {
  /* css for the box... */
}
```

#### Step 3: move the JavaScript
- Copy and paste the JavaScript within the `<script>` tags from `index.html` to `index.js`
- Link the index.js file to the `index.html` file within the `<head>` tags

Hint: the code you are copy-pasting should look like the code below:

```js
/* global $ */
'use strict'
$(document).ready(function(){
  // bouncing box code...             
});
```

#### Step 4: Reflection questions:
Create a new file called `reflections.txt`. Inside, answer the following questions:
- What happens if you load the `index.js` file before the jquery file?
- How is the jQuery file being loaded into this project: direct download or Content Delivery Network (CDN)?

## TODO 3) Refactor `index.js` comment headers
- Rename the first comment header: `"Initialization"`
- Rename the second comment header: `"Core Logic"`
- Copy the comment header and add a third comment header at the bottom: `"Helper Functions"`
- move any code that is not below the correct header (hint: variable declarations should all be in `"Initialization"`)

Hint: your comment headers should look something like this:

```js
/////////////////////////////////////////////////
////////////// INITIALIZATION ///////////////////
/////////////////////////////////////////////////

/////////////////////////////////////////////////
//////////////// CORE LOGIC /////////////////////
/////////////////////////////////////////////////

/////////////////////////////////////////////////
////////////// HELPER FUNCTIONS /////////////////
/////////////////////////////////////////////////
```

## TODO 4) Refactor `update`

_All new functions should be declared in the `Helper Functions` section_

(Look at the top of this document for an example of the process outlined below)

#### Step 1: Identify the main sub-tasks that the `update` function performs.

#### Step 2: For each sub-task:
  1. declare a new function in the `"Helper Functions"` section with a name that describes the sub-task. Note: it is likely that it may not need any parameters
  2. insert a `/* multi-line comment */` above your new helper function that describes the sub-task performed.
  3. identify all code for performing the sub-task and copy-paste it into the new helper function
  4. replace the old code with a call to your new helper function
  
#### Step 3: Check to see if any repeated code be made more abstract/modular?

## TODO 5) Refactor `handleBoxClick`

Follow the steps outlined above in TODO 4 for `handleBoxClick`

## TODO 6) Reflection:
Inside the `reflections.txt` file answer the following questions:
- In your opinion, what are the pros of refactoring your HTML, CSS, and JavaScript into separate files? What are the cons?
- In your opinion, what are the pros of refactoring your JavaScript code into separate functions? What are the cons?


