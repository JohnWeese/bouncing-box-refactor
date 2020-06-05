**Table of Contents**
- [Overview](#overview)
- [Separation of Concerns Example](#separation-of-concerns-example)
- [TODOs](#todos)
  - [TODO 1) Create your file structure](#todo-1-create-your-file-structure)
  - [TODO 2) Refactor the file structure](#todo-2-refactor-the-file-structure)
  - [TODO 3) Reflection](#todo-3-reflection)
  - [TODO 4) Refactor index.js comment headers](#todo-4-refactor-indexjs-comment-headers)
  - [TODO 5) Refactor handleBoxClick for separation of concerns](#todo-5-refactor-handleboxclick-for-separation-of-concerns)
  - [TODO 6) Refactor update for separation of concerns](#todo-6-refactor-update-for-separation-of-concerns)
  - [TODO 7) Reflection](#todo-7-reflection)


# Overview

This project will focus on **refactoring** an old project: Bouncing Box.

> Refactoring is the process of internally restructuring existing code without changing its external behavior

The solution code for bouncing box is linked to this repository in a file called `refactor-me.html`. While the program works (if you were to copy/paste the contents of that file into the HTML tab of a jsbin it would work!), it is not organized in a way that follows the rule of **Separation of Concerns**:

> Every file/module/function should perform one task and one task only.

The first goal of this project is to restructure this project such that HTML, CSS, and JavaScript can each live in their own separate file.

The second goal is to then refactor the JavaScript code such that the core logic of the program can be broken up into smaller pieces and implemented using **Helper Functions**.

> A helper function is a function that performs part of the computation of another function. Helper functions are used to make your programs easier to read by giving descriptive names to computations. They also let you reuse computations, just as with functions in general.

# Separation of Concerns Example

The function below determines the pay for an employee that earns $10/hour with the opportunity to earn overtime. The overtime rate increases as the number of overtime hours goes up: $15/hour for 1-4 hours of overtime, $20/hour for 5-9 hours, and $25/hour for more than 10 hours of overtime.

```js
function calculateWage(overtime) { 
  if (overtime < 5) {
    return (10 * 40) + (overtime * 15);
  }
  else if (overtime < 10) {
    return (10 * 40) + (overtime * 20);
  }
  else {
    return (10 * 40) + (overtime * 25);
  }
} 
console.log(calculateWage(1)); //=> 415
console.log(calculateWage(5)); //=> 500
console.log(calculateWage(10)); //=> 750
```

In this function, there are two main concerns: 
1. determine the range of overtime hours
2. calculate the pay based on the rate for the identified range. 

We can separate these two concerns by adding in a helper function that calculates the pay based on the specified overtime rate:

```js
function pay(overtime, rate) {
  return (10 * 40) + (overtime * rate);
}
```

And then replace the code in `calcualteWage` with a call to this helper function.

```js
function calculateWage(overtime) { 
  if (overtime < 5) {
    return pay(overtime, 15);
  }
  else if (overtime < 10) {
    return pay(overtime, 20);
  }
  else {
    return pay(overtime, 25);
  }
}

// helper function
function pay(overtime, rate) {
  return (10 * 40) + (overtime * rate);
}

console.log(calculateWage(1)); //=> 415
console.log(calculateWage(5)); //=> 500
console.log(calculateWage(10)); //=> 750
```

The result is a more readable program (because the helper function has a descriprtive name) and improves the organization of our code. If an error were to exist in the program, it would be easier to identify. Lastly, if we needed to change something such as the base pay from $10/hour to $12/hour, we would only have to update the `pay` function in one place rather than in three.

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

## TODO 5) Refactor `handleBoxClick` for separation of concerns

We need to first identify the separate concerns of `handleBoxClick`. Then we can create helper functions to handle those concerns individually. Consider the existing code for `handleBoxClick`:

```js
function handleBoxClick() {
  points += 1;
  $('#box').text(points);
  if (speedX >= 0) {
    speedX += 3;
  } 
  else if (speedX < 0) {
    speedX -= 3;
  }
  positionX = 0;
}
```

When the box gets clicked, the following high-level "concerns" need to be dealt with: 
- increase the score and update the number on the box
- increase the speed
- reset the position of the box

**Can you see which statements of this function relate to each of these concerns?**

By adding comments, it will become clearer:

```js
function handleBoxClick() {
  // increase points
  points += 1;            
  $('#box').text(points); 
  
  // increase speed
  if (speedX >= 0) {
    speedX += 3;
  } 
  else if (speedX < 0) {
    speedX -= 3;
  }
  
  // reset the position of the box
  positionX = 0;  
}
```

**Now, for each concern we will create a helper function by following these three steps:**
  1. declare a new function in the `"Helper Functions"` section with a name that describes the concern.
  2. identify all code related to that concern and copy-paste it into the new helper function
  3. replace the old code with a call to your new helper function
  
**In the end, the `handleBoxClick` function should only make calls to helper functions. It should not directly implement any of the code itself**.

## TODO 6) Refactor `update` for separation of concerns

The `update` function will be called every 50 milliseconds (20 times per second) and is responsible for redrawing the box in a new position. In addition, on each frame, the `update` function needs to check to see if the box has moved beyond the left or right boundary. If it has, it will change the direction of the box by multiplying the speed by -1.  

**Now, refactor the `update` function by doing the following:**
1. Use comments to describe the high-level concerns of the `update` function
2. declare a new function in the `"Helper Functions"` section with a name that describes the concern.
3. identify all code related to that concern and copy-paste it into the new helper function
4. replace the old code with a call to your new helper function

## TODO 7) Reflection:
Inside the `reflections.txt` file answer the following questions:
- In your opinion, what are the pros of refactoring your HTML, CSS, and JavaScript into separate files? What are the cons?
- In your opinion, what are the pros of refactoring your JavaScript code into separate functions? What are the cons?


