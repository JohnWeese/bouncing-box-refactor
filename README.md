**Table of Contents**
- [Overview](#overview)
- [Separation of Concerns And Abstraction Example](#separation-of-concerns-and-abstraction-example)
- [TODOs](#todos)
  - [TODO 1) Create your file structure](#todo-1-create-your-file-structure)
  - [TODO 2) Refactor the file structure](#todo-2-refactor-the-file-structure)
  - [TODO 3) Reflection](#todo-3-reflection)
  - [TODO 4) Refactor index.js comment headers](#todo-4-refactor-indexjs-comment-headers)
  - [TODO 5) Refactor update for separation of concerns](#todo-5-refactor-update-for-separation-of-concerns)
  - [TODO 6) Refactor handleBoxClick for separation of concerns](#todo-6-refactor-handleboxclick-for-separation-of-concerns)
  - [TODO 7) Reflection](#todo-7-reflection)


# Overview

This project will focus on **refactoring** an old project: Bouncing Box.

> Refactoring is the process of internally restructuring existing code without changing its external behavior

The solution code for bouncing box is linked to this repository in a file called `refactor-me.html`. While the program works (if you were to copy/paste the contents of that file into the HTML tab of a jsbin it would work!), it is not organized in a way that follows the rule of **Separation of Concerns**:

> Every file/module/function should perform one task and one task only.

The first goal of this project is to restructure this project such that HTML, CSS, and JavaScript can each live in their own separate file.

The second goal is to then refactor the JavaScript code such that the core logic of the program can be broken up into smaller pieces and implemented using **Helper Functions**.

> A helper function is a function that performs part of the computation of another function. Helper functions are used to make your programs easier to read by giving descriptive names to computations. They also let you reuse computations, just as with functions in general.

# Separation of Concerns and Abstraction Example

The main principle of separation of concerns is

> Every file/module/function should perform one task and one task only.

The main principle of abstraction is:

> Hide the complexity of code behind functions, also known as _the API_ (Application Programming Interface)

Consider the following program for validating a user's password. The password must have atleast 8 characters, include a number, and at least 1 upper-case letter:

```js
var pw = prompt("choose a password");
var isValid = false;

// check the length of the password, it must have at least 8 characters
var isLongEnough = false;
if (pw.length >= 8) {
  isLongEnough = true;
}

// check to see if at least one uppercase character is included
var hasUpperCase = false;
for (var i = 0; i < pw.length; i++) {
  if (pw[i].toUpperCase() === pw[i]) {
    hasUpperCase = true;
  }
}

// check to see if the password has at least one number
var hasNumber = false;
for (var i = 0; i < pw.length; i++) {
  if (Number(pw[i]) !== NaN) {
    hasNumber = true;
  }
}

// If the password passes all the tests, return "password valid", otherwise return "password invalid"
if (isLongEnough === false) {
  alert("invalid password");
}
else if (hasUpperCase === false) {
  alert("invalid password");
}
else if (hasNumber === false) {
  alert("invalid password");
}
else {
  alert("valid password");
}
```

If my comments weren't included, this program might be pretty difficult to follow for a beginner programmer. This speaks to the importance of commenting your code!

Even with my comments, this `validatePassword` function is quite complex and has multiple steps that work together to reach the end goal. Because of the complexity of the problem, it makes it quite hard to read. 

Furthermore, if I made a mistake, it might not be immediately clear which step I made the mistake on, I would have to search through the entire function to figure out the mistake. Refactoring this code with separation of concerns and abstraction in mind can help improve the **readability** and **debuggability** of this code. 


When refactoring a project, we can often achieve both of these goals by breaking down the core logic of our program into smaller "helper functions" that each accomplish one step of the whole program. When put together, these helper functions can achieve the same result but our core logic becomes more readable and therefore easier to manage, debug, and grow!

First, identify the distinct steps to validating the password. Can you tell what they are?

Here are the steps I would identify:
1. Determine if the password is long enough
2. Determine if the password has at least one upper-case character
3. Determine if the password has at least one number
4. Determine if the password is valid based on the three tests above

Next, create a _helper function_ for each step above, which are functions designed to _help_ the main function do its job. We can turn one of the steps above into a helper function by moving the code for the step into it's own new function, then calling that function from the core logic function (`validatePassword`). 

Consider how I have refactored the program below. Compare and contrast the two versions of the `validatePassword` function. Which is more readable? How does version 2 demonstrate separation of concerns? 


```js


// Core Logic
////////////////////////////////////////////////////////////////////////

var pw = prompt("choose a password");
if (isLongEnough(pw) === false) {
  alert("invalid password");
}
else if (hasUpperCase(pw) === false) {
  alert("invalid password");
}
else if (hasNumber(pw) === false) {
  alert("invalid password");
}
else {
  alert("valid password");
}

// Helper Functions
////////////////////////////////////////////////////////////////////////

// check the length of the password, it must have at least 8 characters
function isLongEnough(pw) {
  if (pw.length >= 8) { 
    return true; 
  }
  else { 
    return false; 
  }
}

// check to see if at least one uppercase character is included
function hasUpperCase(pw) {
  for (var i = 0; i < pw.length; i++) {
    if (pw[i].toUpperCase() === pw[i]) {
      return true;
    }
  }
}

// check to see if the password has at least one number
function hasNumber(pw) {
  for (var i = 0; i < pw.length; i++) {
    if (Number(pw[i]) !== NaN) {
      return true;
    }
  }
}

```

Separation of concerns and abstraction are principles to program by, not rules that must be followed. For this project, refactoring may seem like overkill. However, as our programs grow, organizing code into `core logic` and `helper functions` improve the the readability of the program and simplify the debugging process.

# TODOs

### _Remember to use `control+c` to copy and `control+v` to paste_

## TODO 1) Create your file structure

#### Step 1: Create your folder / files

Right click on the main folder in your workspace and create a new folder with the name: `bouncing-box-refactor`

<img src="https://github.com/OperationSpark/bouncing-box-refactor/blob/master/img/new-folder.png?raw=true" height="250">

Right click on this new folder and create 3 files in that folder: `index.html`, `index.css`, `index.js`

<img src="https://github.com/OperationSpark/bouncing-box-refactor/blob/master/img/new-file.png?raw=true" height="250">

At this point your file structure should look like this:

![alt text](https://github.com/OperationSpark/bouncing-box-refactor/blob/master/img/file-structure.png?raw=true)

## TODO 2) Refactor the file structure

#### Step 1: Copy code from `refactor-me.html` into `index.html`

**NOTE: DO NOT USE YOUR OLD BOUNCING-BOX PROJECT**

Open up the file `refactor-me.html` linked at the top of this github repository. It contains a solution for bouncing box. Copy the contents of that file into your newly created `index.html` file.

#### Step 2: move the CSS:

Copy and paste the CSS within the `<style>` tags from `index.html` to `index.css`. Do not copy the `<style>` tags themselves. You can delete them once you have copied over the CSS.

Hint: the code you are copy-pasting should look like the code below:

```css
.box {
  /* css for the box... */
}
```

#### Step 3: move the JavaScript

Copy and paste the JavaScript within the `<script>` tags from `index.html` to `index.js`. Do not copy the `<script>` tags themselves. You can delete them once you have copied over the JavaScript.

Hint: the code you are copy-pasting should look like the code below:

```js
/* global $ */
'use strict'
$(document).ready(function(){
  // bouncing box code...             
});
```

#### Step 4: Link `index.js` and `index.css` to `index.html`

At this point, your code should be separated into 3 files. If you were to run your program (in cloud9, right-click on `index.html` and select **Preview**), you would notice that it doesn't work! 

That's because `index.html` is only running the code that it has in its own file. We need to tell it to load in the code written in `index.js` and `index.css`. There are 2 tags that can do this for us: `<link>` and `<script>`

Use your google search powers to look up the following (Hint: include "w3schools" in your search query):
1. `HTML <link> tag`
2. `HTML <script> src attribute`

## TODO 3) Reflection:
Create a new file called `reflections.txt`. Inside, answer the following questions:
- How is the jQuery file being loaded into this project: direct download or Content Delivery Network (CDN)?
- If you load the `index.js` file before the jquery file our program doesn't work. Why? Open the preview in a new tab and look at the console to help you find out why.

## TODO 4) Refactor `index.js` comment headers

Comment headers are incredibly userful for organizing the various components of our program. 

For this project we want the overall structure of `index.js` to look like this:

```js
$(document).ready(function() {

  /////////////////////////////////////////////////
  ////////////// INITIALIZATION ///////////////////
  /////////////////////////////////////////////////

  /* variables and other one-time set up code for the program */

  /////////////////////////////////////////////////
  //////////////// CORE LOGIC /////////////////////
  /////////////////////////////////////////////////

  /* main logic of the program: the update / handleBoxClick functions */

  /////////////////////////////////////////////////
  ////////////// HELPER FUNCTIONS /////////////////
  /////////////////////////////////////////////////

  /* functions for executing sub-tasks of the core logic */

});
```

#### Step 1: Rename the first comment header: `"Initialization"`
#### Step 2: Rename the second comment header: `"Core Logic"`
#### Step 3: Copy the comment header and add a third comment header at the bottom: `"Helper Functions"`
#### Step 4: Move any code that is not below the correct header (hint: variable declarations should all be in `"Initialization"`)

## TODO 5) Refactor `update` for separation of concerns

In this step we will create our first helper functions for the function `update`. Each helper function will implement a sub-task that the `update` function will call in sequence. 

Look at the top of this document for an example of the process outlined below.

_NOTE: All new functions should be declared in the `Helper Functions` section_

#### Step 1: Identify the main sub-tasks that the `update` function performs.

#### Step 2: For each sub-task:
  1. declare a new function in the `"Helper Functions"` section with a name that describes the sub-task. Note: it is likely that it may not need any parameters
  2. identify all code for performing the sub-task and copy-paste it into the new helper function
  3. replace the old code with a call to your new helper function
  
#### Challenge: Can any repeated code be made more abstract/modular?

## TODO 6) Refactor `handleBoxClick` for separation of concerns

Follow the steps outlined above in TODO 5 for `handleBoxClick`

## TODO 7) Reflection:
Inside the `reflections.txt` file answer the following questions:
- In your opinion, what are the pros of refactoring your HTML, CSS, and JavaScript into separate files? What are the cons?
- In your opinion, what are the pros of refactoring your JavaScript code into separate functions? What are the cons?


