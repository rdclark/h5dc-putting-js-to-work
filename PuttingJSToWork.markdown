% Putting Javascript to Work
% Richard Clark
% October 24, 2014

# Introductions

## Who am I?

- Richard Clark
- Head of Global Training, [Kaazing](http://www.kaazing.com)
- Formerly: Apple, General Magic, HP, Verifone, etc.

## Say a little about yourself

>- Who you are
>- What's your background
>- What's one thing you'd like from today?

# Getting started

## First, a little HTML5

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Javascript practice</title>
<h1>Just a practice page</h1>
<script>

</script>
```


# Writing quality Javascript


## If you forget var...
```
function area(r) {
  // note: missing var
  result = Math.PI * (r * r); 
  return result;
}
console.log(area(1)); // 3.1415...
console.log(result); // 3.1415
```
> - the variable becomes _global_



## Preventing accidental global variables
```
function area(r) {
  "use strict";
  result = Math.PI * (r * r); &LeftArrow; becomes an error (no var)
  return result;
}
```
> - `"use strict;"`{.code} enables *strict mode*
> - Makes missing *var* an error
> - Use at start of script or function



## Guidelines

> - `"use strict;"`{.code} at top of file or function
> - `===`{.code} and `!==`{.code} for equality
> - Check code with [JSLint](http://www.jslint.com) or [JSHint](http://www.jshint.com)



## Practice

1. Declare `i = 1;`{.code} in a script (by itself)
2. Show it with `console.log(j)`{.code}
3. What happens when you put `"use strict";`{.code} at the top of the script?
4. What happens when you change `i`{.code} into `var i`{.code}?
5. (Challenge) Declare `var j = 2;`{.code} inside a function. Show it with console.log() inside and outside the function.


## What is Truth?

> - Strict **true** and **false** not required.
> - *Truthy* : number != 0, non-empty string, any object
> - *Falsy* : 0, '' and "", NaN, null, undefined



## Coercion

```
console.log(4 + " is even")
```
> - 4 becomes "4"
> - Javascript converts types as needed



## Comparison

All true (`var n = 4`{.code})

```
n == 4
n == "4"
n != 3
n > 3
n > "3"
```



## Comparison

Also true (`var n = 4`{.code})
```
n
"4"
'4'
'Four score and seven years ago...'
!false
```



## Comparison

All false (`var z = 0; var x;`{.code})
```
z
z != 0
''
null
x
undefined
```



## Strict comparison

```
var n = 4, z = 0;
n === 4 // true
n === 0 // false
n === "4" // false
z === 0 // true
z === null // false
n !== 3 // true
```


## Practice

- Write `isOdd(n)`{.code}
- How short can you make it? (Hint: Use truthiness)
- Write `isEven(n)`{.code} in a short form


# 2a: Working with objects

## Simple objects (redux)

Collection of key-value pairs:

```
var point = {x: 5, y: 3};
var oz = {
  name: "The great and mighty Oz",
  location: "Emerald City",
  behindCurtain: true
};
```

Accessing values:
```
console.log(oz.name);
console.log(oz[name]);
oz.name = "Oz";
```

## Object behaviors

```
var oz = {
  name: "The great and mighty Oz",
  location: "Emerald City",
  behindCurtain: true,
  introduce: function() {
    console.log("I am " + this.name)
  }
};

oz.introduce();
```

## Get/Set

*Not implemented by all browsers*

```
var oz = {
  name: get() { return "The great and mighty Oz" },
  location: get() { return  "Emerald City" },
  behindCurtain: set(hiding) { 
  	if (hiding) alert("Pay no attention to the man behind the curtain!") },
  introduce: function() {
    console.log("I am " + this.name)
  }
};

oz.name = "Glinda the Good" <-- not allowed!
```

## Object terminology

> - **method** = function visible in an object
> - **property** = data (variable) visible in an object
> - **this** used inside an object to get its own methods and properties
> - **accessor** = the get and set methods

## Practice

- Make an object with your name and other information about you
- Add a method that prints your name to the console. Call it.

# Classes

## Another way to make objects

```
var oz = new Object();
oz.name = "The great and mighty Oz";
oz.location = "Emerald City";
```

## Class "Person"

```
function Person(name, location) {
	this.name = name;
	this.location = location;
}

var gandalf = new Person("Gandalf", "Middle Earth");
```

## Making introductions

```
function Person(name, location) {
	this.name = name;
	this.location = location;
}

Person.prototype.introduce = function() {
	console.log("I am " + this.name);
}

var gandalf = new Person("Gandalf", "Middle Earth");
gandalf.introduce();
```

## Wizards are people too

```
function Wizard(name, location, orientation) {
	Person.call(this, name, location);
	this.orientation = orientation;
}

Wizard.prototype = new Person();

Wizard.prototype.isGood = function() { 
  return this.orientation == "good";
}

var gandalf = new Wizard("Gandalf", "Middle Earth", "good");
console.log(gandalf.isGood());
```

## Practice

- Create a class to hold your name 
- Add a method that prints your name to the console. Call it.

# Some built-in classes

## String

```
var greeting = "Hello, World";
console.log(greeting.length); 

var insult = new String("Your mother smells of Elderberries");
console.log(insult.contains("Elderberries"));
```

## Some String methods

[String reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)

- `String.prototype.length` : read-only length
- `String.prototype.contains(*substring*)` : true if *substring* is found within *string*
- `String.prototype.concat(*another_string*)` : same as `string + another_string`
- `String.protoype.trim()` : removes whitespace before and after

## Finding things

```
var s = 'abcd';
s.length; // 4
s[0]; // 'a'
s.indexOf('b'); // 1
s.indexOf('z'); // -1
```

## Array

[Array reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

```
var a = new Array('a', 'b', 'c');
console.log(a); // ['a', 'b', 'c'];
var a2 = ['d', 2, 'e'];
a.length; // 3
a.indexOf('b'); // 1
```

## Manipulating arrays

[Array reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

```
var a = ['a', 'b', 'c']
a[4] = 'd'; // ['a', 'b', 'c', 'd']
a.push('e'); // ['a', 'b', 'c', 'd', 'e']
a.pop(); // returns 'e', now ['a', 'b', 'c', 'd']
```

# 2b: HTML!

## Back to our test page

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Javascript practice</title>
<h1>Just a practice page</h1>
<script>

</script>
```

## Find the \<h1>

```
var h1 = document.querySelector("h1");
```

<aside class="notes">
    Look at this HTML element in the debugger. Common properties. What happens when you change a property.
</aside>


## Another way

```
var headings = document.getElementsByTagName("h1");
var h1 = headings[0];
```

## Playing with color

```
var h1 = document.querySelector("h1");
h1.style.color = 'red';
```

<aside class="notes">
    Look at h1 in the debugger. What styles does it have? Try changing them.
</aside>

## Changing an element

```
var h1 = document.querySelector("h1");
h1.innerHTML = "Look at me!";
```

## Practice

- Put your name in the h1
- Change the color of the h1
- (Extra credit) Change the font of the h1

# Playtime!

## Try this

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Javascript practice</title>
<style>h1 { -webkit-transition : color 5s }
<h1>Just a practice page</h1>
<script>
  document.querySelector('h1').style.color = 'red';
</script>
```

## Super cheap animation

```
var h1 =  document.querySelector('h1');
var color = 'red';
function changeColor() {
	if (color == 'red') 
		color = 'green';
	else
		color = 'red';
	h1.style.color = color;
}

setInterval(changeColor, 5000);
```


# Building interactions

## Start with a button

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Interactive</title>
<button id="b" onclick="alert('Hello!')">Click me!</button>
```

## Click!

```
<button id="b" onclick="alert('Hello!')">Click me!</button>
```

> - `onclick`{.code} defines a handler for a **click event**

## Preferred approach

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Interactive</title>
<button id="b">Click me!</button>
<script>
  var b = document.querySelector('#b');
  b.onclick = function() { alert('Hello!') };
</script>
```
> - Move script out of the button tag

## All the buttons!

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Buttons!</title>
<button id="a">Click me!</button>
<button id="b">Click me!</button>
<button id="c">Click me!</button>
<button id="d">Click me!</button>
<script>
  var buttons = document.querySelectorAll('button');
  for (var i=0; i < buttons.length; i++) {
    buttons[i].onclick = function() { alert('Hello!') };
  }
</script>
```

## Events

An **[Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)** is:

> - Delivered to browser for every action
> - e.g. **click**, **mousedown**, **mouseup**
> - e.g. **keydown**, **keyup**, **resize**

---

An **[Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)** has properties:

> - `event.type`
> - `event.timeStamp`
> - `event.target`
> - (and more)

## Whack-a-button!

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Which button?</title>
<button id="a">A</button>
<button id="b">B</button>
<button id="c">C</button>
<button id="d">D</button>
<script>
  var buttons = document.querySelectorAll('button');
  for (var i=0; i < buttons.length; i++) {
    buttons[i].onclick = function(event) { 
    	alert("Clicked " + event.target.id) 
    };
  }
</script>
```

## Lose the loop

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Which button?</title>
<div id="buttons">
	<button id="a">A</button>
	<button id="b">B</button>
	<button id="c">C</button>
	<button id="d">D</button>
</div>
<script>
  var buttons = document.querySelector('#buttons');
  buttons.onclick = function(event) { 
  	alert("Clicked " + event.target.id) 
  }
</script>

```

## Event bubbling

> - If there's no handler for the target...
> - ...deliver it to the parent.
> - `event.target`{.code} is the original target
> - `event.currentTarget`{.code} is where you registered the handler

## Practice

1. Add more buttons!
2. Try other events (e.g. **mousedown**, **mouseup**, **mouseover**, **mouseout**)
3. Try handling click events on a link.

# The load event

## Party like it's 1999

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
   "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
  <title>Button</title>
  <script>
    var b = document.getElementById('b');
    b.onclick = function() { alert('Hello!') };
  </script>
</head>
<body>
  <button id="b">Click me!</button>
</body>
</html>

```
<aside class="notes">
    Old-school: scripts in the head of the page. The problem is, the button won't exist when that script runs (before the body of the page.) 
</aside>

## Fixing the problem

```
window.onload = function() {
	var b = document.getElementById('b');
	b.onclick = function() { alert('Hello!') };
}
```

## The load event

> - Fired when a resource (and any dependent resources) has been loaded
> - e.g. when you have images, audio, video, etc. to manipulate.

## Clicky images

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Multiple Images (1)</title>
<div id="images">
	<img src="button1.png">
	<img src="button1.png">
	<img src="button1.png">
	<img src="button1.png">
</div>
<script>
window.onload = function() {
  var images = document.querySelector('#images');
  images.onclick = function() { alert('Hello!') };
}
</script>
```

## Practice

1. Find your practice page
2. Wrap the script in a load handler (`window.onload`)
3. (Extra) Use `addEventListener` instead of `onload`

# Forms

## Greetings!

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Greetings</title>
<form>
	<label for="name">What is your name?</label>
	<input type="text" id="name">
</form>
<script>
window.onload = function() {
  var form = document.forms[0];
  form.onsubmit = function() { 
  	var input = form.elements[0];
  	alert('Hello, ' + input.value);
  }
}
</script>
```

## A mystery

1. Enter your name and hit enter.
2. Leave the alert up.
3. Notice your name in the input box.
4. Dismiss the alert
5. What happens to the name field?

## Default actions

> - The browser handles many events itself.
> - The browser gets the event after your handler.
> - Sequence: *your code* --> *browser*
> - *What did the browser do with your form?*

## Keeping the event to yourself

```
form.onsubmit = function(event) { 
	var input = form.elements[0];
	alert('Hello, ' + input.value);
	event.preventDefault();
}
```

## Note: The old way of doing this

```
form.onsubmit = function(event) { 
	var input = form.elements[0];
	alert('Hello, ' + input.value);
	return false; // deprecated
}
```

## Practice

1. Make your name appear in the span

```
<!DOCTYPE html>
<meta charset=utf-8>
<title>Form practice</title>
<form>
	<input type="text" placeholder="What is your name?">
</form>
<p>Welcome, <span id="name">stranger</span>
<script>
window.onload = function() {
  var form = document.forms[0];
  var input = form.elements[0];
  form.onsubmit = function(event) { 
  	// Write this. 
  	// 1. Get the text from the input
  	// 2. Find the span and change its innerHTML
  	// 3. Optional: Reset the input to empty
  }
}
</script>
```

# Speak Javascript like a native

## Please remember three things

1. _Everything_ is an object.
2. References connect objects.
3. Unused objects are deleted (_garbage collected_)

_When in doubt, draw a picture of the objects and their connections_

## What makes Javascript different?

1. "First-class" functions
2. Closures
3. Dynamic `this` 
4. Many ways to create classes

_Inspired by Angus Croll's [Parlez-Vous Javascript](https://speakerdeck.com/anguscroll/parlez-vous-javascript)_

# Functions

## "First-class" functions:

- Can be stored in variables
- Can be passed as function arguments
- Can be returned from other functions

## Functions as variables

```
function foo() { }
```

```
var foo = function() { }
```

```
var o = {
  foo: function() { }
}
```


## Functions as arguments

Find the odd values in a:
```
var oddValues = [];
for (var i=0; i < a.length; a++) { if (a[i] & 1) oddValues.push(a[i]) };
```

```
function isOdd(x) { return (x & 1); } 
var oddValues = a.filter(isOdd);
```
See: [Array iteration methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

## Can be an anonymous function

```
var oddValues = a.filter(function (x) { return (x & 1) } );
```

## Naming anonymous functions for debugging

```
var oddValues = a.filter(function isOdd(x) { return (x & 1) } );
```

## Practice

1. Create an array of numbers
2. Use `Array.map` to create a new array where all the values are doubled.
3. (Extra) Use `Array.reduce` to add up the numbers.

See: [Array iteration methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

# Function closures

## Remember the buttons?

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Clicky!</title>
  <div id="buttons">
	<button id="a">a</button>
	<button id="b">b</button>
	<button id="c">c</button>
	<button id="d">d</button>
  </div>
<script>
  var div = document.querySelector('#buttons');
  div.onclick = function() { alert('Hello!') };
</script>
```

Let's count the clicks.

---

```javascript
var counters = {a: 0, b: 0, c: 0, d: 0};

function clickHandler(event) {
	var id = event.target.id;
	var count = counters[id];
	count = count + 1;
	counters[id] = count;
	event.target.innerHTML = id + " (" + count + ")";
}

div.onclick = clickHandler;
```
<aside class="notes">
    Yes, I'm being verbose. It's a beginners class and I don't want to melt someone's brain by being too terse. Besides, I need to save those brain cells for what's next... 
</aside>

---

Can you do it without the global?

---

## Make a new event handler for each

```
function attachClickHandler(button) {
	var id = button.id;
	var count = 0;
	button.onclick = function(event) {
		count = count + 1; // or count += 1, or count++
		button.innerHTML = id + " (" + count + ")";
    }
}

var buttons = document.querySelectorAll('button')
for (var i = 0; i < buttons.length; i++) {
    attachClickHandler(buttons[i]);
}
```

<aside class="notes">
    This is where C programmers and the like break down and cry. `button`, `id`, and `count` are allocated as regular objects (not on the stack) and the new anonymous function has a reference to them. Even though the parent function goes out of scope, the inner function still has a reference that keeps those values alive. We say the inner function _"closes around"_ the variables.
</aside>

## Another closure example

```
function makeCounter() {
	var x = 0;
	return function () {
	  return ++x;
	}
}

var count = makeCounter();
count(); // 1
count(); // 2
```

<aside class="notes">
    Question for the class: how would you set an initial value?
</aside>

## Practice

1. Write the `makeCounter` example, but pass in an initial value.
2. (Extra) Implement the counting buttons. Can you show the counts elsewhere on the page (e.g. in a `<span>`)?

# Dynamic `this` 

## Another counter example

```
var counter = {
	count: 0,
	handleClick: function(event) { 
		this.count += 1; 
		event.target.innerHTML = event.target.id + " (" + this.count + ")";
	} 
}

button.onclick = counter.handleClick;
```

<aside class="notes">
    This looks like it should work, but doesn't...
</aside>

## `this` is not the object you are looking for

- In an event handler, `this` = `event.target`

## What happens

```
var counter = {
	count: 0,
	handleClick: function(event) { 
	 	console.log(this);
		this.count += 1; 
		event.target.innerHTML = event.target.id + " (" + this.count + ")";
	} 
}
```

- Console: `this = [object HTMLButtonElement]`
- `this.count` === `undefined`
- `this.count += 1` === `NaN`

## Some things become easier

```
var count = 0;
button.onclick = function(event) { 
	count++; 
	this.innerHTML = this.id + " (" + count + ")";
};
```

## Binding `this`

```
var counter = {
	count: 0,
	handleClick: function(event) { 
		this.count += 1; 
		event.target.innerHTML = id + " (" + this.count + ")";
	} 
}

button.onclick = function (event) { 
	counter.handleClick(event);
}

```

<aside class="notes">
    Now button.onclick gets a function that always sets `this` to `counter` before calling `counter.handleClick`.
</aside>

---

Using [bind\(\)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
```
var counter = {
	count: 0,
	handleClick: function(event) { 
		this.count += 1; 
		event.target.innerHTML = id + " (" + this.count + ")";
	} 
}

button.onclick = counter.handleClick.bind(counter);
```

## Wrapping this up

```
function attachClickHandler(button) {
	var counter = {
		count: 0,
		handleClick: function(event) { 
			this.count += 1; 
			event.target.innerHTML = id + " (" + this.count + ")";
		} 
	button.onclick = counter.handleClick.bind(counter);
}

var buttons = document.querySelectorAll('button');
for (var i=0; i < buttons.length; i++) 
  attachClickHandler(buttons[i]);
```

## Practice

1. Step through the final example in the debugger.
2. Explain it to someone else. (Do you both agree?)

# Alternate ways to create classes

## Do we need full classes?

```
function Person(name, location) {
	this.name = name;
	this.location = location;
}

Person.prototype.introduce = function() {
	console.log("I am " + this.name);
}

function Wizard(name, location, orientation) {
	Person.call(this, name, location);
	this.orientation = orientation;
}

Wizard.prototype = new Person();

Wizard.prototype.isGood = function() { 
  return this.orientation == "good";
}
```

## Maybe just an object...

```
var bilbo = {
	name: "Bilbo Baggins",
	location: "The Shire",
	introduce: function() { console.log("I am " + this.name) }
}
```

## We could even make a factory

```
function makePerson(name, location) {
	return {
		name: (name),
		location: (location),
		introduce: function() { console.log("I am " + this.name) }
	}
}

var bilbo = makePerson("Bilbo Baggins", "The Shire");
```

## Prevent the name from changing

```
function makePerson(name, location) {
	return {
		name: get() { return name },
		location: get() { return location },
		introduce: function() { console.log("I am " + this.name) }
	}
}

var bilbo = makePerson("Bilbo Baggins", "The Shire");
bilbo.name = "Smaug" // <-- ERROR!
```

## Extending the object

```
function makeWizard(name, location, orientation) {
	var me = makePerson(name, location);
	me.orientation = get() { return orientation };
	me.isGood = function() { 
  		return this.orientation == "good" 
  	}
  	return me;
}
```

## Make an object with private variables

"The []Module Pattern]()"

```
function makeCounter() {
	return (function() {
		var _count = 0;
		return {
			count: function() { return ++count },
			reset: function() { _count = 0 }
		}
	})();
}

var counter = makeCounter();
counter.count(); // 1
counter.count(); // 2
counter.reset();
counter.count(); // 1

```

## I-I-F-E

```
(function() { ... })()
```

"Immediately Invoked Function Expression"

## Extend the counter

```
function addCallCounter(counter) {
	return (function () {
		var _calls = 0;
		counter.totalCalls = function () { return ++_calls };
		return counter;
	})();
}

var counter = makeCounter();
addCallCounter(counter);
counter.count(); // 1
counter.totalCalls(); // 1
counter.reset();
counter.count(); // 1
counter.totalCalls(); // 2
```

---

## IIFE uses

### You **will** see this pattern. Often.

- Creating and extending classes (e.g. Underscore)
- Creating loadable modules (e.g. AMD)
- Creating namespaces

## Practice

1. Create a new empty object (`{}` or `new Object()`)
2. Create an object with your name and some function (like `greeting`)
3. Wrap the object up in an IIFE and return it.
4. Create a private variable in the IIFE and include it in the object.
5. (Extra) Write a second function to extend the object.


# Playing with data

## Put some data in an object

```
var data = { 
  values: [2, 3, 4, 5];
}
```

## JSON

[JSON specification](http://json.org)
```
var json_data = '{"values": [2, 3, 4, 5]}';
var data = JSON.parse(json_data);
console.log(JSON.stringify(data));
```

<aside class="notes">
JSON (Javascript Object Notation) is just a Javascript data object (no functions) with three simple rules:
1. All keys must be quoted with double quotes.
2. All string values must be quoted with double quotes.
3. The whole thing is a string.
</aside>

## Older Browser?

[https://github.com/douglascrockford/JSON-js](https://github.com/douglascrockford/JSON-js)

## Practice

### Using the browser console.

1. Define an array in Javascript. Encode it into JSON. 
2. Define an object in Javascript. Encode it into JSON.
3. Create a JSON string. Decode it.

# Promises

## Promises simplify asynchronous code

Before:
```javascript
step1(function (value1) {
    step2(value1, function(value2) {
        step3(value2, function(value3) {
            step4(value3, function(value4) {
                // Do something with value4
            });
        });
    });
});
```

## With promises (using Q)

```javascript
Q.fcall(promisedStep1)
.then(promisedStep2)
.then(promisedStep3)
.then(promisedStep4)
.then(function (value4) {
    // Do something with value4
})
.catch(function (error) {
    // Handle any error from all above steps
})
.done();
```

## Networking without promises

```
var ws = new WebSocket("ws://echo.websocket.org");
ws.onopen = function() {
  ws.send("I hear an echo");
}

ws.onerror = function(err) {
  console.log(err.data);
  ws.close();
}

ws.onmessage = function(evt) {
  console.log(evt.data);
}

function send(message) {
  ws.send(message):
}

```

## Easier networking with promises

I would like to do this:

```
  open("ws://echo.websocket.org")
    .then(send("hello, world"))
  	.then(read)
  	.then(print)
  	.catch(function(error) {
  	   console.log("ERROR " + error)
  	 })
  	.finally(close);

```

## Wrapping WebSocket in promises

```
function open(wsurl) {
  return new Q.Promise(resolve, reject) {
    var ws = new WebSocket(wsurl);`

    ws.onopen = function() {
      resolve(ws);
    }

    ws.onerror = function(err) {
      reject(new Error(err.data));
    }
}
```
Usage:
```
  open("ws://echo.websocket.org").then(...
```

## Waiting for an event

```
function read(ws) {
  return new Q.Promise(resolve) {
    
    ws.onmessage = function(evt) {
      resolve(evt.data);
    }
  }
}
```

## Utility functions

```
function close(ws) { ws.close() };

function send(ws) return { function(message) { ws.send(message) }};

function print(message) {
  console.log(message);
}
```

## When to use promises?

- Talking to external services (e.g. via AJAX)
- Local operations that take time (e.g. image loading)

## Image loading example

```
function getImage(url) {

  return new Q.Promise(resolve, reject) {
    var image = new Image(url);
    image.onload = function() {
      resolve(image);
    }
    image.onerror = function(err) {
      reject(err);
    }
  }
}
```

```
  getImage("./button.png").then(function(image) { ... });
```

## Other promise tricks

- `promise.all([array of functions])` acts like `map`, runs all concurrently.
- Serial actions:

```
  var messages = ["Hello", "goodbye"];
  messages.reduce(function(ws, msg) { ws.send(message); return ws }, open("ws://echo.websocket.org"));
```

# Compatibility & Reliability

## A problem...

Not all browsers speak the same language

- Two flavors of Javascript: ES3 vs. ES5
- ...and JScript
- (ES3/JScript: IE < 9)


## Another problem...

Not all browsers <s>speak the same language</s> have the same APIs

- DOM level 2 vs. DOM level 3
- Event model differences

## Solutions

- Compatibility tools: jQuery, ES5-shim, Modernizr
- Testing tools: QUnit, Jasmine, JSTestDriver, Selenium

# jQuery

---

[jQuery.com](http://www.jquery.com)

- Utility library to simplify client-side programming
- Normalizes differences between browsers (*ahem* IE...)
- Provides simple animations
- Simplifies complex tasks (e.g. Ajax)

--- 

## The almighty $

`$()` is the all-purpose function:
- Searches for elements by selector (like querySelector/querySelectorAll)
- Adds utility functions to DOM elements

## Interactivity and animation

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>jQuery Animations</title>
<script src="lib/jquery-2.1.1.js"></script>
<h1>Hello!</h1>
<script>
$(document).ready(function() {
  var h1 = $('h1');

  var b1 = $('<button>Fade in</button>');
  b1.insertAfter(h1);
  b1.click(function() { h1.fadeIn() });
});
</script>
```

## Method chaining

```
var b1 = $('<button>Fade in</button>');
b1.insertAfter(h1);
b1.click(function() { h1.fadeIn() });
```
vs.
```
$('<button>Fade out</button>')
  .insertAfter(h1)
  .click(function() { h1.fadeOut() });
```

## Forms example

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>jQuery Form</title>
<script src="lib/jquery-2.1.1.js"></script>
<form>
	<input type="text" placeholder="What is your name?">
</form>
<p>Welcome, <span id="name">stranger</span>
<script>
$(document).ready(function() {
  var form = $(document.forms[0]); // or $('form')
  var input = $('input');
  form.submit(function(event) { 
  	$('#name').html(input.val());
  	input.val('');
  	event.preventDefault();
  })
});
</script>

```

## Practice

Using the form example:

1. Hide the paragraph when the page first loads.
2. On submit, animate it into view.
3. (Extra) Hide the paragraph if the entered text is empty. (Hint: `if ('')` is the same as `if (false)` )

# QUnit

## Let's test some code

```
<!DOCTYPE html>
<html>
<meta charset="utf-8">
<title>Unit testing</title>
<link rel="stylesheet" href="http://code.jquery.com/qunit/qunit-1.14.0.css">
<div id="qunit"></div>
<script src="http://code.jquery.com/qunit/qunit-1.14.0.js"></script>
<script>
  function average(x, y) {
    return (x + y) / 2;
  }
</script>
<script>
  // ===== Tests =====
  module("Averages");
  
  test("Two values", function() {
    equal(average(2, 4), 3, "Even numbers");
    equal(average(1, 2), 1.5, "Adjacent numbers");
  });
</script>
```

## The setup

```
<!DOCTYPE html>
<html>
<meta charset="utf-8">
<title>Unit testing</title>
<link rel="stylesheet" href="http://code.jquery.com/qunit/qunit-1.14.0.css">
<div id="qunit"></div>
<script src="http://code.jquery.com/qunit/qunit-1.14.0.js"></script>
<!-- Tests here -->
```

## The tests

```
  module("Averages");
  
  test("Two values", function() {
    equal(average(2, 4), 3, "Even numbers");
    equal(average(1, 2), 1.5, "Adjacent numbers");
  });
```

## Testing HTML

```
<!DOCTYPE html>
<meta charset="utf-8">
<title>Table Example</title>
<link rel="stylesheet" href="http://code.jquery.com/qunit/qunit-1.14.0.css">
<div id="qunit"></div>
<div id="qunit-fixture">
	<table id=testTable />
</div>
<script src="http://code.jquery.com/jquery-2.1.1.min.js"></script>
<script src="http://code.jquery.com/qunit/qunit-1.14.0.js"></script>
```

## The code

```
function addRow(numRows) {
  numRows = numRows || 1;
  var table = $('#testTable');
  for (var i=0; i < numRows; i++) {
	  table.append("<tr><td>Data!</td></tr>");
  }
}

// ===== Tests =====

module("Table modification");

test("Initial conditions", function() {
  ok($('#testTable'), "We have the table");
  equal($('#testTable tr').length, 0, "No rows");
});

test("Add one row", function() {
  addRow();
  equal($('#testTable tr').length, 1, "One row");
});
```

## JSTestRunner

- Run tests on multiple browsers concurrently

## Practice

1. Can you implement averaging three numbers? (Write the test, watch it fail, fix the code, watch it pass)
2. Can you average *n* numbers? (Hint: `arguments.length` and `arguments[n]`)
3. (Extra) Add a test fixture







# Graphs and charts

## Introducing D3.js

[D3.js Homepage](http://d3js.org)

## Hello, World using D3

[Tutorial](http://bost.ocks.org/mike/bar/)

```
<!DOCTYPE html>
<meta charset=utf-8>
<title>Hello!</title>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <script>
	var body = d3.select("body");
	var h1 = body.append("h1");
	h1.html("Hello, world!");
  </script>
</body>
```

## Multiple sections

[Tutorial](http://bost.ocks.org/mike/bar/)

```
<!DOCTYPE html>
<meta charset=utf-8>
<title>Hello!</title>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <section></section>
  <section></section>
  <script>
	var sections = d3.selectAll("section");
	var h1 = sections.append("h1");
	h1.html("Hello, world!");
  </script>
</body>
```

## Add some style

[Tutorial](http://bost.ocks.org/mike/bar/)

```
<!DOCTYPE html>
<meta charset=utf-8>
<title>Hello!</title>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <section></section>
  <section></section>
  <script>
	var sections = d3.selectAll("section");
	var h1 = sections.append("h1").style('color', 'red');
	h1.html("Hello, world!");
  </script>
</body>
```

## Let's create a SVG graph

```html
<!DOCTYPE html>
<meta charset=utf-8>
<title>Simple graph (path)</title>
<style>
	svg { border: 1px solid lightgrey }
	.line { fill: none; stroke: steelblue; stroke-width: 1.5px }
</style>
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
<body>
  <svg width=100 height=100 />
  <script>
    var points = [[0, 100], [25, 50], [50, 0], [75, 50], [100, 100]];
	var svg = d3.select("svg");
	var line = d3.svg.line();
	var path = line(points);
	svg.append('path').attr('class', 'line').attr('d', path);
  </script>
</body>
```

## D3 will call `line` if we supply the data

```
var points = [[0, 100], [25, 50], [50, 0], [75, 50], [100, 100]];
var svg = d3.select("svg");
var line = d3.svg.line();

svg.append('path')
	.datum(points)		// remember the points...
	.attr('class', 'line')
	.attr('d', line); 	// calls line(points) on our behalf 
```

## Scaled data, accessors

```
var points = [0, 0.5, 1, 0.5, 0];
var svg = d3.select("svg");
var x = d3.scale.linear().domain([0, points.length - 1]).range([0, 100]);
var y = d3.scale.linear().range([100, 0]);
var line = d3.svg.line()
	.x(function (d, i) { return x(i) } )
	.y(function (d, i) { return y(d) });
svg.append('path').datum(points).attr('class', 'line').attr('d', line);
```

## Practice

1. Take one of the examples, have D3 add the `svg` element dynamically (`.append('svg')`)
2. Set the height and width of that element (see the D3 tutorials)
3. (Extra) Can you graph a set of circles instead?


# Wrapping up

## What we didn't talk about

- Downgrading to ES3
- Lesser-used parts of ES5: propery accessors, `Object.freeze`, `Object.seal`, etc.
- "Monkey Patching"
- ES6 "Harmony"

## What you know now

- Variables, functions, control structures, data types
- Working with objects and `this`
- Working with classes: both via `.prototype` and make-your-own
- Building interactions (with and without jQuery)
- Building visualizations with D3.js
- Testing your code across multiple browsers

## Resources for your journey

- [Eloquent Javascript](http://www.eloquentjavascript.net)
- [Daily JS](http://dailyjs.com)
- [JavaScript, JavaScript](http://javascriptweblog.wordpress.com)
- [YUI Blog](http://www.yuiblog.com/blog)
- Javascript Garden
- [JSLint.com](http://JSLint.com)

---

# Thank you!

e: [richard.clark@kaazing.com](mailto:richard.clark@kaazing.com) t: @rdclark
