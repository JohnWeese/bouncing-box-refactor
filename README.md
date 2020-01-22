# Refactoring Takeaways

### Separation of Concerns
- Every file/module/function should perform one task and one task only.
- If a file/module/function serves multiple purposes, break it into separate files/modules/functions (when appropriate)

### DRY: Don't Repeat Yourself
- Repetitive code presents an opportunity to refactor for abstraction

# TODOs

### _Remember to use control+c and control+v to copy and paste_

### TODO 1) Create your files
- Sign into cloud9
- Create a new folder with the name: `bouncing-box-refactor`
- Create 3 files in that folder: `index.html`, `index.css`, `index.js`
- Copy the code from bouncing box jsbin (see below) into `index.html`

[Bouncing Box jsbin: Right Click --> Open Link in New Tab](https://jsbin.com/goyuhod/edit?html,output)

### TODO 2) Refactor the file structure

#### Step 1: Use your google search powers to figure out:
1. how to add an external css file to an html file
2. how to add a javascript file to an html file

#### Step 2: move the CSS:
- Copy and paste the CSS between the `<style>` tags into `index.css`
- Link the index.css file to the `index.html`file within the `<head>` tags

#### Step 3: move the JavaScript
- Copy and paste the JavaScript between the `<script>` tags into `index.js`
- Link the index.js file to the `index.html` file within the `<head>` tags

#### Step 4: Reflection questions:
Create a new file called `reflections.txt`. Inside, answer the following questions:
- What happens if you load the `index.js` file before the jquery file?
- How is the jQuery file being loaded into this project: direct download or Content Delivery Network (CDN)?

### TODO 3) Refactor `index.js` comment headers
- Rename first comment header: "Initialization"
- Rename second comment header: "Core Logic"
- Copy the comment header and add a third section: "Helper Functions"
- move any code that is not in the correct position (hint: variable declarations should all be in "Initialization")

### TODO 4) Refactor Core Logic

For both the `update` function and the `handleBoxClick` function, follow the steps below. All new functions should be declared in the `Helper Functions` section:

1. Identify the main actions the function performs.
2. For each action:
  - group together all code for performing a distinct action into a consecutive sequence
  - insert a comment describing the action performed by the sequence of code
  - sequences that involve if statements can begin with "check for X" or "did X occur?"
  - declare a new function in the "Helper Functions" section with a name that describes the action. It likely will not need   any parameters
  - copy and paste the sequence of code (not the comment) into your new function
  - replace old code with function call
3. Can any repeated code be made more abstract/modular?

### TODO 5) Reflection:
Inside the `reflections.txt` file answer the following questions:
- In your opinion, what are the pros of separating files? What are the cons?
- In your opinion, what are the pros of refactoring your code into separate functions? What are the cons?


