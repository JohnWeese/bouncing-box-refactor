# Refactoring Principles

### Separation of Concerns
- Every file/module/function should perform one task and one task only.
- If a file/module/function serves multiple purposes, break it into separate files/modules/functions (when appropriate)

### DRY: Don't Repeat Yourself
- Repetitive code presents an opportunity to refactor for abstraction

# TODOs

### _Remember to use `control+c` and `control+v` to copy and paste_

## TODO 1) Create your file structure
- Sign into cloud9
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

## Refactoring Core Logic Example (no coding for this step)

Below is an example of refactoring a "core logic" function. Consider the following code:

```js
// core logic
function greet() {
  // ask for name
  var name = prompt("what is your name?");

  // say hello
  console.log("hello " + name);
  
  // say goodbye
  console.log("goodbye " + name);
} 
```

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

## TODO 4) Refactor `update`

_All new functions should be declared in the `Helper Functions` section_

#### Step 1: Identify the main actions the function performs.
#### Step 2: For each action:
  - group together/separate code by distinct actions performed
  - insert a `//comment` describing the action performed by the sequence of code. Sequences that involve `if` statements can begin with `// check for X` or `// did X occur?`
  - declare a new function in the `"Helper Functions"` section with a name that describes the action. It may not need any parameters
  - copy and paste the sequence of code (not the comment) into your new function's `{ Code Block }`
  - replace old code with a call to your new function
#### Step 3: Can any repeated code be made more abstract/modular?

## TODO 5) Refactor `handleBoxClick`

Follow the steps outlined above in TODO 4 for `handleBoxClick`

## TODO 6) Reflection:
Inside the `reflections.txt` file answer the following questions:
- In your opinion, what are the pros of refactoring your HTML, CSS, and JavaScript into separate files? What are the cons?
- In your opinion, what are the pros of refactoring your JavaScript code into separate functions? What are the cons?


