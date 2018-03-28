# Javascript

>  Note: A collection of notes from the [teamtreehouse.com](teamtreehouse.com) javascript path.


```javascript
var x = 0;
function doSomething() {}

window.onload = function () {} // Runs as soon as the webpage loads.
<script src="scripts.js"></script> // Loads a js file
var answer = prompt('What color is the moon?'); // Capture input

// Concatenate strings
'Hello' + ' ' + 'World';

// Convert values
parseInt()
parseFloat()

// Error
throw new Error('error message');

isNan();

// Array
var names = ['Jim', 'John', 'Jane'];
names.push('Tim'); // Appends items
names.unshift('Tom'); // Adds items to the beginning of an array.
names.shift(); // Remove first item
names.pop(); // Remove last item

var allNames = names.join(', '); // Combines array into a string
var combineArrays = array1.concat(array2); // Combines arrays in one
var index = names.indexOf('John'); // Returns the position of the item or -1

// Two-dimensional array
var array = [
  [1, 2, 3],
  [4, 5, 5]
]

array[1][1]

// Object literal
var student = {
  name: 'Dave',
  graes: [99, 89, 93, 73]
};

student[name]; // Access property value
student.name; // Access property value (preferred)
student[name] = 'Will' // Assign prperty values
student.name = 'Will' // Assign prperty values (preferred)

// Iterating over an object
for (var prop in person) {
 // Must use bracket notation to access the value 
 console.log(prop, ': ', person[prop]); 
}
```



## ES6

```javascript
const pi = 3.14159;
let name = 'Will';

// const doesn't prevent complex objects from being modified.
// let has block level scoping
```



#### Template literals

```javascript
// Template literal (backticks)
`<ui> 
	<li></li>
 </ul>
`

// String interpolation
`Hello, ${name}, nice to see you.`

${name} // dynamic value
```



### Arrow function syntax

```javascript
// Shorter syntax
const sayHello = () => {
  console.log("Hello");
}

// Arrow function with arguments
const cube = (x) => {
  return square(x);
}

// Even more concise for single argument functions
// Remove curly braces for single line functions
// remove the return for an implied return of the last line.
const sqaure = x => x * x;

// Callbacks
function Person() {
  this.age = 0;
  var self = this;
  setInterval(function() {
    self.age ++;
  }, 1000);
}

// or

function Person() {
  this.age = 0;
  setInterval(() => {
    this.age ++;
  }, 1000);
}
```



## JavaScript and the DOM

```javascript
// Document Object Model
window
document

const heading = document.getElementById('heading');

heading.addEventListener('click', () => {
  heading.style.color = 'red';
});

// Use the value property to get the text that has been entered into an input element.
input.value

// getElementsByTagName
document.getElementsByTagName() // returns a collection

// getElementsByClassName
document.getElementsByClassName() // returns a collection
```



### Query selector

```
document.querySelector('li'); // Returns the first matching selector
document.querySelectorAll('.error');
document.querySelectorAll('li:nth-child(even)');
```

https://babeljs.io/

https://caniuse.com



### Text elements

```javascript
textContent
innerHTML // can change the html of an element
```

### Changing Element Attributes

```javascript
input.type // displays an element's type
input.className // displays an element's description
p.title = "Some new title";
```

### Creating elements

```javascript
document.createElement('p');
```

### Appending nodes

```javascript
ul.appendChild(li) // Adds the element to the page
```

### Removing nodes

```javascript
ui.removeChild(li); // Removes the element from the page
```



## Functions as parameters

```javascript
function exec(func, arg) {
  func(arg);
}

exec(someFunc, 'Some argument');

// Anonymous function
exec((something) => {
  
});

// Callback function
window.setTimeout((something) => {
  console.log(something);
}, 3000, 'Greetings, everyone!');
```



### Event objects

```javascript
ul.addEventListener('click', (e) => {
  console.log(e.target);
});

ul.addEventListener('click', (e) => {
  if (e.target.tagName === 'LI') {
    // Do something
  }
});
```



## Traversing the DOM

```javascript
// Get the parent node
let li = event.target;
let ul = li.parentNode;

// previousElementSibling and insertBefore
li.previousElementSibling;
parentNode.insertBefore(newNode, referenceNode);

// nextElementSibling
li.nextElementSibling;

// Get all children of a node
ul.children;

// First and last element child
ul.firstElementChild
ul.lastElementChild
```



## Dom Scripting

```javascript
form.addEventListener('submit', (e) => {
  e.preventDefault(); // Prevents the browser from refreshing.
  console.log(input.value);
});

// DOMContentLoaded is a listener that only runs the javascript once the page has been loaded.
document.addEventListener('DOMContentLoaded', () => {   
});

// Object functions
const action = button.textContent;
      
const nameActions = {
  remove: () => {
    ul.removeChild(li);
  },

  edit: () => {
    const span = li.firstElementChild;
    const input = document.createElement('input');
    input.type = 'text';
    input.value = span.textContent;
    li.insertBefore(input, span);
    li.removeChild(span);
    button.textContent = 'save';
  },

  save: () => {
    const input = li.firstElementChild;
    const span = document.createElement('span');
    span.textContent = input.value;
    li.insertBefore(span, input);
    li.removeChild(input);
    button.textContent = 'edit';
  }
};

// Select and run action in button name
nameActions[action]();
```

