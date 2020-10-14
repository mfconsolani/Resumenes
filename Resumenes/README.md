# Introduction to JavaScript

Created in 1995 by _Netscape Communicator_ willing to write actions to their website. 

At some point in history, it was needed to specify a standard way of using JavaScript. **For that, it was created ECMAScript, better known as ES.**

#### JAVASCRIPT TYPES

1. ```Number```

* 2+2, 2/2, 2*2, 2%2

2. ```String```

* ```"Mauro"```
* ```'Mauro'```
* ```"Hello" + " there!"```
* ```'This isn\'t very nice'```   
    * Scape Character with ```\```

* ```10 + "34"``` results in ```"1034"``` 
    * Javascripts detects a number added to a string and converts it into a string guessing the user means to add two strings together

* ```10 - "3"``` results in ```7``` 
    * Javascripts detects a number subtracting a string and converts it into a number given that you can never subtract a number to a string
* ```"hello" - "bye"``` results in ```Nan``` which means **Not a Number**

3. ```Boolean```
    
    Pay attention: there is no capital letter at the beginning as a diference with Python

* ```true``` 
    * ```3 > 2``` results in ```true```
    * ```5 >= 5``` results in ```true```

* ```false```
    * ```3 < 2``` results in ```false```

4. ```Undefined```

It's used when nothing is assigned to a variable; **means that the variable has not been assigned**

Undefined most typically means a variable has been declared, but not defined. For example:

```js
let b;
console.log(b);
// undefined
```

5. ```Null```

It represents the value for "_nothing_"

There are two features of ```null``` you should understand:

* ```null``` is an empty or non-existent value.

* ```null``` must be assigned.


6. ```Symbol``` (new in ECMAScript 6)

By specification, object property keys may be either of string type, or of symbol type. Not numbers, not booleans, only strings or symbols, these two types.


**A “symbol” represents a unique identifier.**

A value of this type can be created using ```Symbol()```:

```js
// id is a new symbol
let id = Symbol();
```

Upon creation, we can give symbol a description (also called a symbol name), mostly useful for debugging purposes:

```js
// id is a symbol with the description "id"
let id = Symbol("id");
```

Symbols are guaranteed to be unique. Even if we create many symbols with the same description, they are different values. The description is just a label that doesn’t affect anything.

For instance, here are two symbols with the same description – they are not equal:

```js
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

[More about Symbol()](https://javascript.info/symbol)

7. ```Object```

Objects are collections of property (seems to be like a dictionary in Python).

```js
var user = {
    name: 'John',
    age: 34,
    country: 'Argentina',
    isMarried: false,
    nickNames: ['Johny', 'Joh', 'John'],
    shouts: function () {
        console.log("AAAAAAAAAAHHHH")
    }
};

user['name']; // This returns 'John'. Python wise.
user.name;   // This also returns 'John'. Like accessing to a Python object property
user.nickNames[1]; // This would return 'Joh'
user.shouts() //This returns "AAAAAAAAAAHHHH"
```

>A function like ```user.shouts``` inside an object is called a ```method```. Thats what ```methods```: they are functions inside an object; functions related/associated to an object.

```js
var list = [
    {
        user: 'Mauro',
        password: 'Secret',
    },
    {
        user: 'Wan',
        password: 'Uknown'
    }

];

list[1].password; // This returns "Uknown"

```

**Adding new properties to the object**

```js

user.hobby = 'Soccer'; 
// OR
user['hobby2'] = 'VolleyBall';

```


#### JAVASCRIPT COMPARISONS

1. ```!==```

Means **not equal to**
* ```3 !== 4``` results in ```true```
* ```3 !== 3``` results in ```false```

2. ```===``` 

Means **equal to**. This is needed when you are comparing two things:
* ```3 === 3``` results in ```true```
* ```3 = 3``` results in ```false```

3. ```>=```
4. ```<=```
5. ```>```
6. ```<```


#### JAVASCRIPT VARIABLES

Allows us to catch and hold values. 

1. ```var```

Variables can't start with numbers. _Example:_ ```var 3 = 3``` results in an ```Error```. But, ```var three = 3``` works fine.

*   Variables need to start with a letter
*   Variables can't start with a symbol
*   Variables **can sometimes** start with a ```$``` or a ```_```
*   If the variable is composed by two words or more, should use camel case style. Example ```firstName = 'Mauro'```

```js
var first = prompt('Enter first number');
var second = prompt('Enter second number');
var sum = Number(first) + Number(second);
```

2. ```let``` (new in ECMAScript 6)

The key difference between ```var``` and ```let``` lies in their scopes. ```var``` is function scoped while ```let``` is block scoped. 
Any time ```let``` is wrapped around brackets, it creates a new scope. While if you use ```var``` it only creates a new scope if it's
used inside a function; otherwise, it exists in the global scope. 


The example below which will highlight the block scope for let more clearly: 

```js
let mango = "yellow"

if (mango === "yellow"){
  let mango = "blue"
  console.log(mango)
}
console.log(mango)
```

**Using ```let```**
```mango``` is declared as "yellow" in line 1, and redeclared as "blue" in line 4 - inside the ```if``` block. However, as the output shows, the ```mango``` declared inside the ```if``` block has scope within that block only. Outside this block, the original ```mango``` variable set to "yellow" is available.


```js
var mango = "yellow"

if (mango === "yellow"){
  var mango = "blue"
  console.log(mango)
}
console.log(mango)
```

**Using ```var```**
Conversely, in the code that uses ```var```, redeclaration of mango to "blue" inside the ```if``` block, also changes the ```mango``` declared in line 1 to "blue". This is because **variables declared with ```var``` are defined globally, regardless of block scope.**

_Additional Note:_
>Use ```let``` as a general rule, and ```var``` on occasion. Block scoping is the standard and most readable choice, and will make debugging easier. Block scoping makes it easy to see exactly where a variable is in scope. Function scoping makes things a lot less apparent, and much easier to accidentally introduce bugs with scoping mistakes. In general, the smaller the scope you can use, the better. Thus ```let``` over ```var```. Also, there is less risk of memory leaks due to variables staying in memory long after they have become irrelevant


3. ```const``` (new in ECMAScript 6)

Las variables constantes presentan un ámbito de bloque (block scope) tal y como lo hacen las variables definidas usando la instrucción ```let```, con la particularidad de que el valor de una constante no puede cambiarse a través de la reasignación. Las constantes no se pueden redeclarar.

```js
const PI = 3.141592653589793;
PI = 3.14;      // This will give an error
PI = PI + 10;   // This will also give an error
```

```js
const a = function() {
    console.log("this is a function declared in a constant variable. You can't reasign me")
}
```

**Constant Objects can Change**

```js
// You can create a const object:
const car = {type:"Fiat", model:"500", color:"white"};

// You can change a property:
car.color = "red";

// You can add a property:
car.owner = "Johnson";
```

But you can NOT reassign a constant object:

```js
const car = {type:"Fiat", model:"500", color:"white"};
car = {type:"Volvo", model:"EX60", color:"red"};    // ERROR
```

**Constant Arrays can Change**

You can change the elements of a constant array:

```js
// You can create a constant array:
const cars = ["Saab", "Volvo", "BMW"];

// You can change an element:
cars[0] = "Toyota";

// You can add an element:
cars.push("Audi");
```

But you can NOT reassign a constant array

```js
const cars = ["Saab", "Volvo", "BMW"];
cars = ["Toyota", "Volvo", "Audi"];    // ERROR
```

#### JAVASCRIPT CONDITIONALS

1. ```if```

```js
if (name === 'Billy') {
    alert('Hi Billy!');
}
```

2. ```else```

```js
if (name === "Billy") {
    alert("Hi Billy!");
} else {
    alert("I don't know you");
}
```

3. ```else if```

```js
if (name === 'Billy') {
    alert('Hi Billy!');
} else if (name === 'Susan') {
    alert('Hi Susan!');
} else {
    alert('I dont know you');
}
```

4. ```ternary operator```

**Syntax**

```condition ? expression 1 : expression 2```
*Is this true or false? If it's true, provide expression 1, else, provide expression 2.*

Example 1:

```js
function isUserValid(bool) {
    return bool;
}

var answer = isUserValid(true) ? "You may enter" : "Access Denied"
```
Example 2:

```js
var automatedAnswer = "Your account number is " + ( isUserValid(false) ? "1234" : "not available");
```

5. ```switch```

A switch statement can replace multiple if checks. It gives a more descriptive way to compare a value with multiple variants.
The switch has one or more case blocks and an optional default.

```js
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

This is how it works:

* The value of x is checked for a strict equality to the value from the first case (that is, value1) then to the second (value2) and so on.
* If the equality is found, switch starts to execute the code starting from the corresponding case, until the nearest break (or until the end of switch).
* If no case is matched then the default code is executed (if it exists).

```js
function moveCommand(direction) {
    var whatHappens;
    switch (direction) { //switch statement checks direction parameter; 
        case "forward":   // if direction equals forward
            whatHappens = "You encounter a monster"; // do this
            break;                                  // and then break the switch statement
        case "back":   // if direction equals back
            whatHappens = "You arrived home"; // do this
            break;                                  // and then break the switch statement
        case "right":   // if direction equals right
            whatHappens = "You found a river"; // do this
            break;                                  // and then break the switch statement
        case "left":   // if direction equals left
            whatHappens = "You run into a troll"; // do this
            break;                                  // and then break the switch statement
        default: 
            whatHappens = "Please enter a valid direction";
    } 
    return whatHappens;
}
```


#### JAVASCRIPT LOGICAL OPERATORS

1. _And_ operator: ```&&```

```js
if (firstName === 'Mauro' && secondName === 'Consolani') {
    alert('Hola ' + firstName + " " + secondName);
} else {
    alert('Have no clue who the hell you are');
}
```

2. _Or_ operator: ```||```

```js
if (name === 'Billy' || name === 'Ann') {
    alert('Hi Billy or Ann!');
} else if (name === 'Joe') {
    alert('Hi Joe');
} else {
    alert('I dont really know who you are. Sorry!');
}
```

3. _Not_ operator: ```!```

```js
if (!(name === 'Billy')) {
    alert('Hi somebody but for sure not Billy!');
}
```

*   ```!true``` returns ```false```
*   ```!false``` returns ```true```


#### JAVASCRIPT FUNCTIONS

1. **Function Expression**

***Function expressions always end with a semicolon***

_Syntax:_

```js
var a = function name() {};
```

_Example:_

```js
var sayBye = function() {
    console.log('See you later!');
};

sayBye(); //This actually calls the function
```

_Additional Note:_
>This kind of functions are called **Anonymous Functions**. You refer to them with a variable (the function is assigned to variable) but they don't have an actual name as opposed to _Function Declaration_.
>In some very specic times, you can assign a name to **Anonymous Functions**:
```js
var bye = function sayBye() {
    console.log("Bye dude");
};
```

2. **Function Declaration**

_Syntax:_

```js
function name() {}
```
_Example:_

```js
function sayHello() {
    console.log('Helloooooooo!');
}

sayHello(); //This actually calls the function
```

_Additional Notes:_

>* **Functions with arguments:** You can add arguments to function following the next syntax:
```js
function askForSong(song) {
    console.log('You asked for:' + song);
}

askForSong('Paradise, by Cold Play');
```

>* **```return``` value:** If you don't return any value or don't use a function which by default returns a value (i.e. console.log()), the function will display "_undefined_"
```js
function noReturn(a, b) { 
    a * b;                  //WRONG WAY
}

noReturn(5,10)
undefined                   //result
```

```js
function noReturn(a, b) { 
   return a * b;           //CORRECT WAY
}

noReturn(5,10)
50                         //result
```

3. ```return```

Likewise in Python, return ends the function as well as it returns whichever value is meant to be return. Else, it will return _undefined_ 

```js
function multiply(a,b) {
    if (a > 10 || b > 10) {
        return "that's a complex one!";
    } else {
        return a * b;
    }
```

_Additional Note:_
>*  **Concatenating functions example:**

```js
function multiply(a, b) {
        return a * b;
    }

alert(multiply(a,b));
```

4. 

```js
()  // => (new in ECMAScript 6)
``` 

#### JAVASCRIPT DATA STRUCTURES

1. ```Array```

Is a way to store and organize information. Arrays have some built-in methods. 

>Why aren't arrays also a JavaScript data type? Well... When you inspect an array it looks like this: 
```js
array
(3) ["Kiwi", "Oranges", "Blueberries"]
0: "Kiwi"
1: "Oranges"
2: "Blueberries"
length: 3
__proto__: Array(0)
```
>The left side looks just like the name of the property and the right side the value of that property. So an array is basically an object.


```js
var list = ['tiger', 'lion', 'bird']; // array declaration
var numbers = [1, 2, 3, 4, 5];
var booleans = [true, false, true, true, false];
var functionList = [function apple() {
    console.log("This is an apple!");
}]
var mixedList = [3, true, undefined, 'tiger', function apple() {
    console.log("This is an apple!");
}];

console.log(list[1]); // Accessing to the array
```

**Built-in Array Methods**:
>Some of them at least...

* ```list.shift();```: pops the **first** element from the array from and it actually ```return``` the shifted item.
* ```list.pop();```: pops the **last** element from the array from and it actually ```return``` the popped item.
* ```list.push("item");```: appends the "item" at the **end** of the array. It returns the quantity (_length_) of elements in the array.
* ```list.concat(['bee', 'deer']);```: concatenates the list passed as an argument with the array that called the method. Returns the array with the added elements/array.
* ```list.sort();```: Sorts the items in the array. Returns the sorted array.
* ```list.reverse();```: Reverse the order of the items from the array.
[Array Methods - W3Schools ](https://www.w3schools.com/jsref/jsref_obj_array.asp)



2. ```Object```

Objects are collections of property (seems to be like a dictionary in Python).

```js
var user = {
    name: 'John',
    age: 34,
    country: 'Argentina',
    isMarried: false,
    nickNames: ['Johny', 'Joh', 'John'],
    shouts: function () {
        console.log("AAAAAAAAAAHHHH")
    }
};

user['name']; // This returns 'John'. Python wise.
user.name;   // This also returns 'John'. Like accessing to a Python object property
user.nickNames[1]; // This would return 'Joh'
user.shouts() //This returns "AAAAAAAAAAHHHH"
```

>A function like ```user.shouts``` inside an object is called a ```method```. Thats what ```methods```: they are functions inside an object; functions related/associated to an object.

```js
var list = [
    {
        user: 'Mauro',
        password: 'Secret',
    },
    {
        user: 'Wan',
        password: 'Uknown'
    }

];

list[1].password; // This returns "Uknown"

```

**Adding new properties to the object**

```js

user.hobby = 'Soccer'; 
// OR
user['hobby2'] = 'VolleyBall';

```



**Built-in Array Methods**:
>Some of them at least...

```js


```


#### JAVASCRIPT LOOPING

1. ```for```

```js
for (var i = 0; i < list.length; i++) {
    console.log(i);                 
}
```
This functions says that: _make a counter called ```i```. While ```i``` is smaller than the length of ```list```, add 1 to ```i``` in each loop._ 

_Example:_

```js
var todos = [
    "clear room", 
    "brush teeth", 
    "eat healthy", 
    "excersice", 
    "learn javascript"
];

for (var i = 0; i < todos.length; i++) {
    todos[i] = todos[i] + '!';
}

var todosLength = todos.length
for (var i = 0; i < todosLength; i++) {
    todos.pop();
}
```


2. ```while```

The ```while``` loop checks the condition first while the ```do while``` loop checks the condition after the ```do```. 

```js
var counterOne = 10;
while (counterOne > 0) {
    console.log(counterOne);
    counterOne--
}
``` 

3. ```do``` 

It says: _do this as long as the condition set in the ```while``` applies; then, break_

The ```while``` loop checks the condition first while the ```do while``` loop checks the condition after the ```do```.

```js
var counterTwo = 10;
do { 
    console.log(counterTwo);
    counterTwo--;
} while (counterTwo > 0);
```

4. ```forEach``` (new in ECMAScript 5) 

```js
var todos = [
    "clear room", 
    "brush teeth", 
    "eat healthy", 
    "excersice", 
    "learn javascript"
];

todos.forEach(function(todo, index) {
    console.log(todo, i);
})

//returns 
// clear room 0
// brush teeth 1
// eat healthy 2
// excersice 3
// learn javascript 4

//You can also do the same like this

function logTodos(todo, i) {
    console.log(todo, i);
}

todos.forEach(logTodos);
```


#### JAVASCRIPT KEYWORDS

```break```
```case```
```catch```
```class```
```const```
```continue```
```debugger```
```default```
```delete```
```do```
```else```
```export```
```extends```
```finally```
```for```
```function```
```if```
```import```
```in```
```instanceof```
```new```
```return```

```super```:

In JavaScript classes, you need to always call ```super``` when defining the constructor of a subclass. All React component classes that have a constructor should start with a ```super(props)``` call.

```switch```
```this```
```throw```
```try```
```typeof```
```var```
```void```
```while```
```with```
```yield```

_Console Useful Functions:_

>Clear console with: ```clear()```

>Generate a popup box that takes an input (like ```input()``` in python): ```prompt('What is you name?')```. ```prompt()``` turns content into a string. Must convert data type after in case you need to.

>Generate a popup box with a printed message: ```alert('Whatever message you want to show in the popup')```


##### Semicolon ;

**In Javascript, a semicolon means the end of an expression**. *An expression is something that produces a value.* With a statement, you don't need to add semicolons.

```js
if (name === 'Billy') {
    alert('Hi Billy!');
}
```

```js
if (name === 'Billy') //This is an Statement
```

```js 
{
    alert('Hi Billy!'); //This is an expression; produces a value. 
}
```

## DOM - Document Object Model

When a web page is loaded, the browser creates a Document Object Model of the page.

The HTML DOM model is constructed as a tree of Objects.

With the object model, JavaScript gets all the power it needs to create dynamic HTML:

* JavaScript can change all the HTML elements in the page
* JavaScript can change all the HTML attributes in the page
* JavaScript can change all the CSS styles in the page
* JavaScript can remove existing HTML elements and attributes
* JavaScript can add new HTML elements and attributes
* JavaScript can react to all existing HTML events in the page
* JavaScript can create new HTML events in the page


_Example:_ 

* ```document``` command in the console displays the DOM information (the HTML Tree Object). 
* ```window``` command in the console displays the windows information. Thus, ```alert()``` also work if you call it like ```windows.alert()```, because ```window``` is its _parent_. If you don't specify the ```window``` object, the browser asumes that you are calling ```alert()``` inside the ```window```, displaying the message in the browser's window.  
* ```document.write("Hellooooo");``` this creates an HTML that displays "Hellooooo". If you try ```window.write()``` it won't work because ```write``` is a property of ```document```, and ```document``` is a property of ```window```


So, a _web browser_, has a ```window``` object, that has a property ```document```, that specifies what to get displayed. To decide that, the DOM reads the HTML and CSS and then JavaScript (the engine) reads line by line and if it ever needs to change anything, JS can "speak" with the ```document``` object and modify the HTML and CSS. 


**Web Browsers allow us to access the DOM through the ```document``` object. The ```window``` object is the _parent_ of the ```document``` object.**  

Each browser has their own JavaScript engine. They look at the JS file and execute it line by line. 

1. Chrome: _V8_
2. Edge: _ChakraCore_
3. Safari: _Nitros_
4. Mozilla: _SpiderMonkey_


The ```document``` has methods that allow DOM manipulation, such as:

1. ```var li = document.createElement("li")```

2. ```li.appendChild()```

Append a child element of the element where the method is used in. In this case, a child of ```li```

3. ```li.appendChild(document.createTextNode("testing"))``` 

This create a string with the word "testing" inside the ```<li>``` tag

### DOM Selectors

**Remember that some of these DOM Selectors return an array; thus, it's necessary to indicate the index you want to access to the array when accessing from third party functions to avoid errors or eventually loop over the elements.**

1. ```getElementsByTagName```

```js
document.getElementsByTagName("h1");
```

2. ```getElementsByClassName```

```js
document.getElementsByClassName("second");
// HTMLCollection [p.second]
```
To access the actual element you can do the following: 

```js
document.getElementsByClassName("second")[0]
```


3. ```getElementById```

```js
document.getElementById("first");
```

4. ```querySelector``` 

The ```Document``` method ```querySelector()``` returns **the first** ```Element``` within the document that matches the specified selector, or group of selectors. If no matches are found, ```null``` is returned.

```js
document.querySelector("h1")
document.querySelector("li")
```

5. ```querySelectorAll```

The ```Document``` method ```querySelectorAll()``` returns a static (not live) ```NodeList``` representing a list of the document's elements that match the specified group of selectors. Once the ```NodeList``` of matching elements is returned, you can examine it just like any array.

**You can query more than one element at the time: look at the examples below**

```js
document.querySelectorAll("li")

document.querySelectorAll("li, h1")
// NodeList(7) [h1, li, li, li, li, li, li]
```

_Additional Note:_
>Andrei Neagoie recommends the use of querySelector and querySelectorAll for general use.

#### Get and Set tag attributes

To get or set attribute, first we have to target the element (select the desired element)

1. ```getAttribute```

```js
document.querySelector("li").getAttribute("random");
```


2. ```setAttribute```

```js
document.querySelector("li").setAttribute("random", "1000");
// >undefined

document.querySelector("li");
//> <li random=​"1000">​Notebook​</li>​
```

#### Changing Styles

Every element has a ```style``` property which you can check like this: 

```js
document.querySelector("h1").style;
// >CSSStyleDeclaration {alignContent: "", alignItems: "", alignSelf: "", alignmentBaseline: "", all: "", …}
```

1. ```style.{property}``` //ok

This will modify the style in the inline way; straight in the HTML which as we know is not the best practice. 

```js
document.querySelector("h1").style.background = "yellow";
```

2. ```className``` //best

```js
var h1 = document.querySelector("h1");

h1.className = "display-4"
//> "display-4"
```
>This changes the style of the ```h1``` because Bootstrap CDN is linked at the .html file. 


3. ```classList``` //best

The ```Element.classList``` is a read-only property that returns a live ```DOMTokenList``` collection of the ```class``` attributes of the element. This can then be used to manipulate the class list.

Using ```classList``` is a convenient alternative to accessing an element's list of classes as a space-delimited string via ```element.className```.

```js
document.querySelector("li").classList;
// >DOMTokenList(2) ["red", "blue", value: "red blue"]
// >0: "red"
// >1: "blue"
// >length: 2
// >value: "red blue"
// >__proto__: DOMTokenList
```
This ```classList``` method enables some other methods, as shown below.


I. ```classList.add```

```js
document.querySelector("li").classList.add("shadow");

// or

document.querySelector("li").classList.add("done"); // this adds a line-through the text
```

II. ```classList.remove```

```js
document.querySelector("li").classList.remove("shadow");
```

III. ```classList.toggle```

It's like a switch that turns ON or OFF a class based on its actual value. If the class is ON (```true```), it turns it OFF (```false```)

```js
document.querySelector("li").classList.toggle("done");
```

```toggle( String [, force] )```

* Cuando sólo hay un argumento presente: Alterna el valor de la clase; ej., si la clase existe la elimina y devuelve ```false```, si no, la añade y devuelve ```true```.

* Cuando el segundo argumento está presente: Si el segundo argumento se evalúa como ```true```, se añade la clase indicada, y si se evalúa como false, la elimina.

[ClassList Methods - MDN Documentation](https://developer.mozilla.org/es/docs/Web/API/Element/classList)


#### Bonus

1. ```innerHTML``` //DANGEROUS

Changes the actual content inside the tags.

```js
document.querySelector("h1").innerHTML = "<strong>!!!!!!!</strong>"
```
If you check the tag content now it would look like this:

```js
document.querySelector("h1");
// <h1>​<strong>​!!!!!!!​</strong>​</h1>​
```

2. ```parentElement```

Enables access to the parent element of the actual selection.

```js
document.querySelector("li").parentElement

/* 
<ul>​
    <li class=​"red blue" random=​"23">​Notebook​</li>
    ​<li>​Jello​</li>
    ​<li>​Spinach​</li>
    ​<li>​Rice​</li>
    ​<li>​Birthday Cake​</li>
    ​<li>​Candles​</li>
</ul>​
*/

//or

document.querySelector("li").parentElement.parentElement
// <body>​…​</body>​
```


3. ```children```

Enables access to the children elements of the actual selection.

```js
document.querySelector("ul").children

// >HTMLCollection(6) [li.red.blue, li, li, li, li, li]

//or

document.querySelector("li").parentElement.parentElement.children

// >HTMLCollection(5) [h1, p#first, p.second, ul, script, first: p#first]

```

**It is important to CACHE selectors in variables**

### Events

Events are things like clicking, mouse entering or hovering, user trying something on a searchbar. 
We can listen to this events and react to them using JavaScript.

_Additional Note:_ 
>DOM Events are sent to notify code of interesting things that have taken place. **Each event is represented by an object** which is based on the ```Event``` interface, and may have additional custom fields and/or functions used to get additional information about what happened. Events can represent everything from basic user interactions to automated notifications of things happening in the rendering model.

[Events - MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/Events)

#### Event Listener

```addEventListener()``` accepts two parameters and allows JS to see or listen for changes in the DOM.

1. The event to listen to, i.e.: ```"click"```

2. The action that is going to be performed afterwards: ```function() { console.log("clicking!"); }```

>It's highly important to add the index of the element in the array you want to access to when targetting elements; else, you are going to get an error

```js
var button = document.getElementsByTagName("button")[0];

button.addEventListener("click", function() {
    console.log("Clicking!!");
})
```

Can also do the same to count the times the mouse enter the button (is like hovering basically):

```js
button.addEventListener("mouseenter", function() {
    console.log("Clicking!!");
})
```

or when the mouse leaves the button

```js
button.addEventListener("mouseleaves", function() {
    console.log("Clicking!!");
})
```

_Additional Note:_
>Everytime an ```addEventListener``` method is added, we have two arguments: the event to listen to, i.e.: ```"keypress"``` and the function to execute when the event is being listened. That function also receives automatically and implicitly the event as an argument. Try this to see the event:

```js
var input = document.getElementById("userinput");
var button = document.getElementById("enter");
var ul = document.querySelector("ul");


button.addEventListener("click", function() {
    if (input.value.length > 0) {
        var li = document.createElement("li");
        li.appendChild(document.createTextNode(input.value));
        ul.appendChild(li);
        input.value = "";
    }
})

input.addEventListener("keypress", function(event) {
    console.log(event);
})

/*
KeyboardEvent {isTrusted: true, key: "k", code: "KeyK", location: 0, ctrlKey: false, …}
altKey: false
bubbles: true
cancelBubble: false
cancelable: true
charCode: 107  <<<<<<<<<<<<<<<<<<<<--------------------------------------------------
code: "KeyK"
composed: true
ctrlKey: false
currentTarget: null
defaultPrevented: false
detail: 0
eventPhase: 0
isComposing: false
isTrusted: true
key: "k"
keyCode: 107    <<<<<<<<<<<<<<<<<<<<--------------------------------------------------
location: 0
metaKey: false
path: (5) [input#userinput, body, html, document, Window]
repeat: false
returnValue: true
shiftKey: false
sourceCapabilities: InputDeviceCapabilities {firesTouchEvents: false}
srcElement: input#userinput
target: input#userinput
timeStamp: 70197.36999995075
type: "keypress"
view: Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …}
which: 107  <<<<<<<<<<<<<<<<<<<<--------------------------------------------------
__proto__: KeyboardEvent
*/
```

**With ```event.which``` or ```event.keyCode``` or ```event.charCode``` you can access to the events character code to then compare it to the key you need for the function to work.**

_____ 

**Event example**


```js
var input = document.getElementById("userinput");
var button = document.getElementById("enter");
var ul = document.querySelector("ul");


function inputLengthTrue() {
    if (input.value.length > 0) {
        return true
    }
}

function createListElement() {
    var li = document.createElement("li");
    li.appendChild(document.createTextNode(input.value));
    ul.appendChild(li);
    input.value = "";
}

function addListAfterClick() {
    if (inputLengthTrue()) {
        createListElement();
        }
    }

function addListAfterEnter(event) {
    if (inputLengthTrue() && event.keyCode === 13) {   // 13 is the keyCode for Enter key 
        createListElement();                        // event.which or event.charCode work fine also
    }
}

button.addEventListener("click", addListAfterClick); //No parenthesis;

input.addEventListener("keypress", addListAfterEnter); // No parenthesis;
```

_____


###  Callback Functions
In the previous video you saw something interesting:

Event listener syntax : 
```js
button.addEventListener("click", addListAfterClick);
input.addEventListener("keypress", addListAfterKeypress);
```

You didn't see the function being called like this as you may have expected: 

```js
button.addEventListener("click", addListAfterClick());
input.addEventListener("keypress", addListAfterKeypress(event));
```

This is something called a callback function. When that line of javascript runs, we don't want the addListAfterClick function to run because we are just adding the event listener now to wait for click or keypress. We want to let it know though that we want this action to happen when a click happens. So the function now automatically gets run (gets added the ()) every time the click happens. So we are passing a reference to the function without running it.

### Event Delegation, Bubbling and Capturing

_Event delegation is the technique, bubbling is what the event itself does, and capturing is a way of using event delgation on events that don’t bubble._

#### Event Delegation

Event delegation is a technique for listening to events where you delegate a parent element as the listener for all of the events that happen inside it.

For example, if you wanted to detect any time any field changed in value inside a specific form, you could do this:

```js
var form = document.querySelector('#hogwarts-application');

// Listen for changes to fields inside the form
form.addEventListener('input', function (event) {

	// Log the field that was changed
	console.log(event.target);

}, false);
```

#### Event Bubbling

Bubbling is what the event itself does.

If you’ve ever watched the bubbles in a glass of soda, you’ll understand how event bubbling works.

The event starts are the element that triggered it. Then, it bubbles up to each of it’s parent elements until it reaches the html element.

Using a form field as an example, the event would bubble up to the parent form, then any containers or divs the form was in, then the body, then the html element, then the document, then the window.

Any listeners on any of those parent elements would get triggered as it bubbles up.

#### Event Capturing

Most events bubble. But some, like the ```focus``` event, do not.

```js
document.addEventListener('focus', function (event) {
	console.log(event.target);
}, true);
```

You can focus on things over and over again, but the event callback will never run.

There’s a trick you can use to capture the event, though. The last argument in addEventListener() is called useCapture. We almost always set it to false.

For events that don’t bubble, set it to true to capture the event anyways.


_Additional Note:_
>I typically recommend using event delegation for event listeners instead of attaching them to individual elements.
>Common question: Isn’t it bad for performance to listen to every click in the document.??
>Amazingly, it’s actually better for performance to use this approach.
>Every event listener you create uses memory in the browser. It’s “cheaper” for the browser to track one event and fire it on every click that it is to manage multiple events.
>If you’re only listening for events on a single element, feel free to attach directly to that element. But if you’re listening for events on multiple elements, I’d recommend using event delegation.
>**As an added benefit, you can dynamically add elements to the DOM later and your event listener will catch them too, since it checks for the selector when the event fires rather than ahead of time**

### Scope

#### Root Scope

Means what variables I have access when the code is running. By default in JS you are in the ```root``` scope, which is the ```window``` object.

```js
function winFunc() {
    console.log("this is now defined in the global scope, and if you run me and inspect me, u'll find me as a window method");
}

// winfunc: ƒ winfunc()
```

**This is called the _root_ scope**

Functions can have access to variables in the ```root``` scope but not the other way. 

#### Child Scope

```js 
function notWindowVariable() {
    var a = "hello";
}

// var a can just be accessed inside the function, not ouside. It only lives in the function scope
```

### Desctructuring

[Destructuring props](https://medium.com/@gazzaazhari/destructuring-props-in-react-d8f163d3ef84)

La sintaxis de asignación desestructurante (destructuring assignment) es una expresión que posibilita la extracción de datos de arrays, o de propiedades de objetos, en variables distintas.

Destructuring was introduced in ES6. It’s a JavaScript feature that allows us to extract multiple pieces of data from an array or object and assign them to their own variables.

Example for React:

```js
const { monsters, searchField } = this.state;
//That is equal to:

const monsters = this.state.monsters;
const searchField = this.state.searchField;
```

```js
let a, b, rest;
[a, b] = [10, 20];

console.log(a);
// expected output: 10

console.log(b);
// expected output: 20

[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// expected output: Array [30,40,50]
```

Syntax: ```const { player, experience } = obj;```


```js
const obj = {
    player: "Bobby",
    experience: 100,
    wizardLevel: false
} 

const player = obj.player;
const experience = obj.experience;
let wizardLevel = obj.wizardLevel;

// This below is destructuring

const { player, experience } = obj; // <------- This is destructuring
let { wizardLevel } = obj;
```

### Object Properties dynamic

**Case 1:**

```js
const name = "john snow";

const obj = {
    [name]: "hello",
    ["ray" + "smith"]: "hihi",
}
```

**Case 2:**

```js
const a = "Simon";
const b = "true";
const c = {};

// if you want the property to match the value, you can do this:
const obj = {
    a,  // instead of a:a
    b,  // instead of b:b
    c   // instead of c:c
}
```

### Template Strings

Like formatting strings in Python!

Must right everything within the back ticks! ---> `` 

```js
const name = "Sally";
const age = 34;
const pet = "Horse";

const greetingBest = `Hello ${name} you seem to be ${age-10}. What a lovely ${pet}`; 
```

### Default Arguments

```js
function greet(name='', age=30, pet="cat") {
    return greetingBest = `Hello ${name} you seem to be ${age-10}. What a lovely ${pet}`;
}
```


### Arrow Functions

[Arrow Functions](https://javascript.info/arrow-functions-basics)

```js
function add(a,b) {
    return a+b;
}

add(1,2);

// the above is the same as:

const add2 = (a, b) => a + b;

add2(1+2);
```

There’s another very simple and concise syntax for creating functions, that’s often better than Function Expressions.

It’s called “arrow functions”, because it looks like this:

```js
let func = (arg1, arg2, ...argN) => expression
```

This creates a function ```func``` that accepts arguments ```arg1..argN```, then evaluates the ```expression``` on the right side with their use and returns its result.

In other words, it’s the shorter version of:

```js
let func = function(arg1, arg2, ...argN) {
  return expression;
};
```

_Example:_ 
```js
let sum = (a, b) => a + b;

/* This arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3
```

As you can, see ```(a, b) => a + b``` means a function that accepts two arguments named ```a``` and ```b```. Upon the execution, it evaluates the expression ```a + b``` and returns the result.


**If only one parameter is passed**

If we have only one argument, then parentheses around parameters can be omitted, making that even shorter.

For example:

```js
let double = n => n * 2;
// roughly the same as: let double = function(n) { return n * 2 }

alert( double(3) ); // 6
```

**If none parameters are required**

If there are no arguments, parentheses will be empty (but they should be present):

```js
let sayHi = () => alert("Hello!");

sayHi();
```

**Arrow functions can be used in the same way as Function Expressions.**

For instance, to dynamically create a function:

```js
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello') :
  () => alert("Greetings!");

welcome();
```

**Multiline arrow function**

The examples above took arguments from the left of ```=>``` and evaluated the right-side expression with them.

Sometimes we need something a little bit more complex, like multiple expressions or statements. It is also possible, but we should enclose them in curly braces. Then use a normal ```return``` within them.

Like this:

```js
let sum = (a, b) => {  // the curly brace opens a multiline function
  let result = a + b;
  return result; // if we use curly braces, then we need an explicit "return"
};

alert( sum(1, 2) ); // 3
```

## Advanced Functions

[Advanced Functions - ZTM Video](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8691784#overview)

### Closures

[Closures for noobs](https://www.codingame.com/playgrounds/6516/closures-in-javascript-for-beginners)

Child scopes, always have access to parent scopes.

*Closures is just saying a function ran, the function executed, is never going to execute again buy it's going to remember that there are references to their variables, so their childscope always have access to the parent scope*

Whenever a function is invoked, a new scope is created for that call. The local variable declared inside the function belong to that scope – they can only be accessed from that function.

When the function has finished the execution, the scope is usually destroyed. A simple example of such function is this:

```js
function buildName(name) { 
    var greeting = "Hello, " + name; 
    return greeting;
}
```

It doesn’t get more simple than that. The function ```buildName()``` declares a local variable greeting and returns it. Every function call creates a new scope with a new local variable and after the function is done executing, we have no way to refer to that scope again, so it’s garbage collected.

But how about when we have a link to that scope? 

```js
function buildName(name) { 
    var greeting = "Hello, " + name + "!"; 
    var sayName = function() {
        var welcome = greeting + " Welcome!";
        console.log(greeting); 
    };
    return sayName; 
}

var sayMyName = buildName("John");
sayMyName();  // Hello, John. Welcome!
sayMyName();  // Hello, John. Welcome!
sayMyName();  // Hello, John. Welcome!
```

The function ```sayName()``` from this example is a closure.

A closure is a function which has access to the variable from another function’s scope. This is accomplished by creating a function inside a function. Of course, the outer function does not have access to the inner scope.

The ```sayName()``` function has it’s own local scope (with variable welcome) and has also access to the outer (enclosing) function’s scope. It this case, the variable greeting from ```buildName()```.

After the execution of ```buildName``` is done, the scope is not destroyed in this case. The ```sayMyName()``` function still has access to it, so it won’t be garbage collected. However, there is not other way of accessing data from the outer scope except the closure.

This is the big gotcha of the entire concept. The closure serve as the gateway between the global context and the outer scope. I cannot access directly variables from the outer scope if the closure is not allowing it. This way, I can protect the variables from the outer scope. They are – by all means – private and the closure can serve as a getter or setter for them.

**Important!**

* Closure are nested function which has access to the outer scope

* After the outer function is returned, by keeping a reference to the inner function (the closures) we prevent the outer scope to be destroyed.

Through closure, you can achieve real private data in Javascript. The closure is the gateway between the outer scope and the rest of the program. It can choose what data to expose and what not.

### Currying

```js
const multiply = (a,b) => a * b;

// Here goes the curried function

const curriedMultiply = (a) => (b) => a * b;
curriedMultiply(2)(3);
// 6

curriendMultiply(3);
//(b) => a * b
```

[Currying Information](https://javascript.info/currying-partials)

Process of converting a function that takes multiple arguments into a function that takes them one at a time

Currying is a transformation of functions that translates a function from callable as ```f(a, b, c)``` into callable as ```f(a)(b)(c)```.

Currying doesn’t call a function. It just transforms it.

Let’s see an example first. We’ll create a helper function ```curry(f)``` that performs currying for a two-argument ```f```. In other words, ```curry(f)``` for two-argument ```f(a, b)``` translates it into a function that runs as ```f(a)(b)```:

```js
function curry(f) { // curry(f) does the currying transform
  return function(a) {
    return function(b) {
      return f(a, b);
    };
  };
}
// usage
function sum(a, b) {
  return a + b;
}

let curriedSum = curry(sum);

alert( curriedSum(1)(2) ); // 3
```

As you can see, the implementation is straightforward: it’s just two wrappers.

The result of ```curry(f)``` is a wrapper ```function(a)```.

When it is called like ```curriedSum(1)```, the argument is saved in the Lexical Environment, and a new wrapper is returned ```function(b)```.
Then this wrapper is called with ```2``` as an argument, and it passes the call to the original ```sum```.

### Compose

[Function Composition](https://www.codementor.io/@michelre/use-function-composition-in-javascript-gkmxos5mj)

Compose is the act of putting two functions together to form a third function where the output of one function is the input of one other.

_Function composition is a mechanism of combining multiple simple functions to build a more complicated one. The result of each function is passed to the next one._

```js
const compose = (f, g) => (a) => f(g(a));

const sum = (num) => num + 1;

compose(sum, sum)(5);
// 7 
```


Simple Example

```js
const add = (a, b) => a + b;
const mult = (a, b) => a * b;
add(2, mult(3, 5))
```

____ 

## Web Dev fundamentals

1. **Avoiding side effects**: try to avoid functions affecting the "outside world". 

2. **Functional Purity**: We always return something in our functions. 

**By avoiding side effects and always returning something we create something that we call *deterministic*. It means that no matter what, the return value it will be always the same. When we say "the same value" we mean that if your function is meant to return a letter from the alphabet, it will always do so, no matter which letter but it will be a letter and never a number; a letter. Thus, we know that "this function is in charge of returning a letter from the alphabet".**

____

## Advanced Arrays

```js
const array = [1, 2, 3, 4, 5];
const double = []
const newArray = array.forEach( (num) => {
    double.push(num * 2);
})

console.log(double)
// [2, 4, 6, 8, 10]
```

### Advanced Array Methods

#### Map

**Map expects you to always ```return``` something**

```map``` vs ```forEach```

* ```map``` **creates a new array** with the results of calling a provided function on every element in the calling array. The difference is that ```map()``` utilizes return values and actually returns a new ```Array``` of the same size.

* ```forEach``` It executes a provided function once for each array element. Just loops through something and does whatever the functions says to. The ```forEach()``` method doesn’t actually return anything (it returns ```undefined```). It simply calls a provided function on each element in your array. This callback is allowed to mutate the calling array.

```js
const array = [1, 2, 3, 4, 5];

const mapArray = array.map( (num) => {
    return num * 2;
})


```

#### Filter

What if you have an array, but only want some of the elements in it? That’s where ```.filter()``` comes in! Basically, if the callback function returns true, the current element will be in the resulting array. If it returns false, it won’t be.

```js
const array = [1, 2, 3, 4, 5];

const filterArray = array.filter( num => {
    return num > 3;
})
```

```js
var pilots = [
  {
    id: 2,
    name: "Wedge Antilles",
    faction: "Rebels",
  },
  {
    id: 8,
    name: "Ciena Ree",
    faction: "Empire",
  },
  {
    id: 40,
    name: "Iden Versio",
    faction: "Empire",
  },
  {
    id: 66,
    name: "Thane Kyrell",
    faction: "Rebels",
  }
];

const rebels = pilots.filter(pilot => pilot.faction === "Rebels");
const empire = pilots.filter(pilot => pilot.faction === "Empire");

```

#### Reduce

[Video on Reduce Function](https://www.youtube.com/watch?v=g1C40tDP0Bk)

Reduce takes two arguments; the callback function to implement, and the default value for the accumulator. If not default value is passed, accumulator will be set to the first element in the array.

```js
const array = [1, 2, 10, 16];

const reduceArray = array.reduce((accumulator, num) => {
    return accumulator + num;
}, 0); // this is the accumulator default value
```

Reduce comes with some terminology such as _reducer_ & _accumulator_. The _accumulator_ is the value that we end with and the _reducer_ is what action we will perform in order to get to one value. You must remember that a reducer will only return one value and one value only hence the name reduce.
 
Just like ```.map()```, ```.reduce()``` also runs a callback for each element of an array. What’s different here is that **reduce passes the result of this callback (the accumulator) from one array element to the other.**
The accumulator can be pretty much anything (integer, string, object, etc.) and must be instantiated or passed when calling ```.reduce()```.

Time for an example! Say you have an array with these pilots and their respective years of experience:

```js
var pilots = [
  {
    id: 10,
    name: "Poe Dameron",
    years: 14,
  },
  {
    id: 2,
    name: "Temmin 'Snap' Wexley",
    years: 30,
  },
  {
    id: 41,
    name: "Tallissan Lintra",
    years: 16,
  },
  {
    id: 99,
    name: "Ello Asty",
    years: 22,
  }
];
```
We need to know the total years of experience of all of them. With ```.reduce()```, it’s pretty straightforward:

```js
const totalYears = pilots.reduce((acc, pilot) => acc + pilot.years, 0);
```
Notice that I’ve set the starting value as ```0```. I could have also used an existing variable if necessary. After running the callback for each element of the array, reduce will return the final value of our accumulator (in our case: ```82```).  


## Advanced Objects

### Reference Type

[Reference Type vs. Primitive Type](https://itnext.io/javascript-interview-prep-primitive-vs-reference-types-62eef165bec8)

When you create an object, that value is not directly assigned to the variable. Instead, a reference to that value is what gets set. All that variable knows about is the location of the object in memory, not the object itself.

* _Primitives_ are copied by their value. **By saying that primitive types are passed by value we mean that we copy a value and we create that value somewhere else in memory**s

* _Objects_ are copied by their reference in memory


### Context

[```this``` for newbies](https://medium.com/@NinjaJavaScript/javascript-this-keyword-explained-simply-e90762d4945d)

[Gentle explanation of ```this```](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)

Context tells you where we are within the object. 

Let's talk about ```this```:

```js
console.log(this === window);
true

this.alert("hello")
``` 

What ```this``` means is what is the object environment that we are in right now. The easiest way to think about it is what is at the left of the dot:

```js
window.alert("hello")
```
In this case, to the left we find the ```window``` object. So doing ```window.alert("hello")``` or doing ```this.alert("hello")``` is the same thing. ```this``` refers what object is inside of.

```js
function a() {
    console.log(this);
}

a();

// Window object is shown
```
This is because the function turns into a ```window``` method. So if you do ```window.a()```, the window object is shown.


```js
const object4 = {
    a: function() {
        console.log(this);
    }
}

object4.a()

// {a: ƒ}
// a: ƒ ()
// __proto__: Object
```

### Instantiation 

Instances or copies of an object. 

```js
class Player {
    constructor(name, type) {
        console.log(this);
        this.name = name;
        this.type = type;
    }

    introduce() {
        console.log(`Hi I am ${this.name}, I'm a ${this.type}`);
    }
}

class Wizard extends Player { //any time we extend something, we need to also call the constructor function of the Playe
    constructor(name, type) { // with super with the properties we wanna pass to the constructor
        super(name, type)
    }
    play() {
        console.log(`I am a ${this.type}`);
    }
}

const wizard1 = new Wizard('Shelly', 'Healer');
const wizard2 = new Wizard('Bob', 'Sorcerer');
```

### Pass by Value vs Pass by Reference

* __Primitive Types__ are inmutable. We can't change them; if you want to change them, we need to completly remove the variable value, meaning, overriding it. Strings, Symbol, Null, Boolean, Integer, all of them are primitive types. You make copies of them through their value, which is stored in memory. **By saying that primitive types are passed by value we mean that we copy a value and we create that value somewhere else in memory**

* __Reference Types__ are stored in memory and the reference type variable only know in which part of the memory space the data is stored.

#### Cloning an object/array without modifying it

##### ```concat``` method

El método ```concat()``` se usa para unir dos o más arrays. Este método no cambia los arrays existentes, sino que devuelve un nuevo array.

```js
const array1 = ['a', 'b', 'c'];
const array2 = ['d', 'e', 'f'];
const array3 = array1.concat(array2);

console.log(array3);
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

```js
let c = [1,2,3,4,5];
let d = [].concat(c); // concat pushes to the empty array a copy of the array in c

d.push(7)
// 6
console.log(d)
// (6) [1, 2, 3, 4, 5, 7]
```


##### ```Object.assing()``` method

El método ```Object.assign()``` copia todas las propiedades enumerables de uno o más objetos fuente a un objeto destino. Devuelve el objeto destino. 

Syntax: 
```js
const returnedTarget = Object.assign(target, source);
```

* ```target```: El objeto destino.

* ```source```: Los objetos origen.


```js
let obj = {a: 1, b: 2, c: 3, d: 4};
let clone = Object.assign({}, obj);
```

##### Spread Operator

[Spread Operator](https://livecodestream.dev/post/2020-05-23-how-to-use-the-spread-operator-in-javascript/)

ES9 has introduced many new features into JavaScript, among them the spread operator (```...```), **which expands an iterable object into a list of its individual elements.**

The spread operator is a useful and quick syntax for adding items to arrays, combining arrays or objects, and spreading an array out into a function’s arguments.

_Example:_

**Making a copy of an array**

```js
const listC = [1, 2, 3]
const listD = [...listC]
```
In this case, **by using the spread operator we are making a new copy in memory of the array, so when we update ```listD``` we are not affecting by any means ```listC```.**


```js
function myFunction(x, y, z) { }
const args = [0, 1, 2];
myFunction(...args);
```

Syntax: 

```js
// For function calls:
myFunction(...iterableObj);

// For array literals or strings:
[...iterableObj, '4', 'five', 6];

//For object literals (new in ECMAScript 2018):
let objClone = { ...obj };
```

**Merging arrays**

```js
const list1 = [1, 2, 3]
const list2 = [4, 5]

const mergedList = [...list1, ...list2]
``` 

_Additional Note:_
>**Shallow Clone:**
>The spread operator won’t do a deep copy, but it would take each of the elements in the original object/list and would map them to a new position in memory. However, if one of the elements happened to be a reference to another object, it will simply make a copy of the reference into memory, but it won’t change what it’s referenced to.

**Deep Cloning to fix Shallow Cloning**:

[Deep Cloning](https://medium.com/javascript-in-plain-english/how-to-deep-copy-objects-and-arrays-in-javascript-7c911359b089)

For objects and arrays containing other objects or arrays, copying these objects requires a deep copy. Otherwise, changes made to the nested references will change the data nested in the original object or array.

##### Deep Cloning with JSON

```js

let obj = {
    a: 'a',
    b: 'b',
    c: {
        deep: 'try and copy me'
    }
};

let superClone = JSON.parse(JSON.stringify(obj))
// {a: "a", b: "b", c: {…}}
// a: "a"
// b: "b"
// c:
// deep: "try and copy me"
```

**Alert:** 
* JSON parser might generate performance issues when deep cloning huge objects.

### Type Coercion

[Type Coercion](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/#:~:text=Type%20coercion%20is%20the%20process,Symbol%20(added%20in%20ES6).)

[JavaScript Equality - Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/)

Type coercion is the process of converting value from one type to another (such as string to number, object to boolean, and so on). Any type, be it primitive or an object, is a valid subject for type coercion. To recall, primitives are: number, string, boolean, null, undefined + Symbol (added in ES6).


In JavaScript, type coercion happens when we use the double equal ```==```. **The double equal means: compare two different values and if they are different types, try to coerce one into the same type as the other**. As to triple equal, it means: compare two values, and if they are different types, don't coherce the values. 

```js
1 === '1'
//False
```

#### Implicit vs. explicit coercion

**Explicit**

* When a developer expresses the intention to convert between types by writing the appropriate code, like ```Number(value)```, it’s called explicit type coercion (or type casting).

**Implicit**

* Since JavaScript is a weakly-typed language, values can also be converted between different types automatically, and it is called implicit type coercion. It usually happens when you apply operators to values of different types, like ```1 == null```, ```2/’5'```, ```null + new Date()```, or it can be triggered by the surrounding context, like with ```if (value) {…}```, where value is coerced to boolean.

**One operator that does not trigger implicit type coercion is ```===```, which is called the strict equality operator. The loose equality operator ```==``` on the other hand does both comparison and type coercion if needed.**


### ```Object.is```

[Equality Comparisons and sameness](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

**Syntax:**

```js
Object.is(value1, value2)
```


```Object.is()``` method is used to determine whether two values are the same or not. Two values can be same if they hold one of the following properties:

* If both the values are undefined.
* If both the values are null.
* If both the values are true or false.
* If both the strings are of the same length with the same characters and in the same order.
* If both the values are numbers and both are “+0”.
* If both the values are numbers and both are “-0”.
* If both the values are numbers and both are “NaN” or both non-zero and both not NaN and both have the same value.

```Object.is()``` takes two arguments which are the values to be compared and returns a boolean indicating whether the two arguments are same or not.

**Difference between ```Object.is()``` method and ```==``` operator**

The “==” and “===” operator treats the number values “+0” and “-0” as equal whereas ```Object.is()``` method treats them as not equal. Apart from that the “==” and “===” operator does not treat ```Number.Nan``` equal to ```Nan```.

**Applications:**

```Object.is()``` is used for comparison of two strings.
```Object.is()``` is used for comparison of two numbers.
```Object.is()``` is used for comparing the polarity of two numbers.
```Object.is()``` is used for comparison of two objects.

## EcmaScript 7 - ES7

#### includes() method

The ```includes()``` method determines whether a string contains the characters of a specified string. This method returns ```true``` if the string contains the characters, and ```false``` if not. The ```includes()``` method is case sensitive.

**Syntax:**

```js
string.includes(searchvalue, start)
```

* ```searchvalue```: Required. The string to search for
* ```start```:  Optional. Default 0. At which position to start the search

_Example:_

```js
var str = "Hello world, welcome to the universe.";
var n = str.includes("world", 12);
```

```js
const pets = ['dog', 'cat', 'horse', 'fish'];
const contains = pets.includes("cat");
```

#### Exponential operator

```js
const cube = (x) => x**3

cube(2);
// 8
``` 

## ECMAScript 8 - ES8

### String Padding

[String Padding](https://codeburst.io/learn-javascript-es-2017-string-padding-padstart-padend-88e90783e7de)

#### .padStart()

**Padding is applied to the left (beginning) side of the string.**

Let’s look at a simple example. Below, we’ll be working with the string 'cat' . Only one parameter is required — the length of the resulting string. As you’ll see, we can optionally provide a second variable — the string to pad with:

```js
'cat'.padStart(5);         // '  cat'
'cat'.padStart(5, 'a');    // 'aacat'
```

Below are some advanced use cases. Note that if the string is initially longer than the padStart() length, nothing is appended to the string:

```js
'cat'.padStart(1, 'a');    // 'cat'
'cat'.padStart(5, 'abc');  // 'abcat'
'cat'.padStart(8, 'abc');  // 'abcabcat'
```


#### .padEnd()

**Padding is applied to the right (ending) side of the string.**

Again, the only difference here is that the string is applied to end of our current string. We’ll use the same examples as above:

```js
'cat'.padEnd(5);         // 'cat  '
'cat'.padEnd(5, 'a');    // 'cataa'
```

Similarly, our advanced examples:

```js
'cat'.padEnd(1, 'a');    // 'cat'
'cat'.padEnd(5, 'abc');  // 'catab'
'cat'.padEnd(8, 'abc');  // 'catabcab'
```

### Trailing commas in function parameter lists and calls

Trailing commas (sometimes called "final commas") can be useful when adding new elements, parameters, or properties to JavaScript code. If you want to add a new property, you can simply add a new line without modifying the previously last line if that line already uses a trailing comma. This makes version-control diffs cleaner and editing code might be less troublesome.

**Arrays**
**JavaScript ignores trailing commas in arrays**:

```js
var arr = [
  1, 
  2, 
  3, 
];

arr; // [1, 2, 3]
arr.length; // 3
```

**Objects**
Starting with ECMAScript 5, **trailing commas in object literals are legal** as well:

```js
var object = { 
  foo: "bar", 
  baz: "qwerty",
  age: 42,
};
```

**Parameter definitions** 

The following function definition pairs are legal and equivalent to each other. Trailing commas don't affect the length property of function declarations or their arguments object.

```js
function f(p) {}
function f(p,) {} 

(p) => {};
(p,) => {};
```

### ```Object.values```

ES2017 introduces a new method called ```Object.values()``` that allows you to return an array of own enumerable property’s values of an object.

```Object.values(obj)``` – returns an array of values.

The ```Object.values()``` accepts an object and returns its own enumerable property’s values as an array. See the following example:

```js
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25
};

const profile = Object.values(person);

console.log(profile);

// [ 'John', 'Doe', 25 ]
```

```js
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25
};

Object.values(person).forEach(value => {
    console.log(value);
})

// John
// Doe
// 25

```

### ```Object.entries```

ES2017 introduces the ```Object.entries()``` method that accepts an object and returns own enumerable **string-keyed property** ```[key, value]``` pairs of the object.

**Important!** 
If they are not string-keyed value pairs, the method won't return that value pair.

```Object.entries(obj)``` – returns an array of ```[key, value]``` pairs.

```js
const ssn = Symbol('ssn');
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25,
    [ssn]: '123-345-789'
};

const kv = Object.entries(person);

console.log(kv);

// [
//     ['firstName', 'John'],
//     ['lastName', 'Doe'],
//     ['age', 25]
// ]
```

In this example:

The ```firstName```, ```lastName```, and ```age``` are own enumerable string-keyed property of the ```person``` object, therefore, they are included in the result. The ```ssn``` is not a string-key property of the person object, so it is not included in the result.

```js
const person = {
    firstName: 'John',
    lastName: 'Doe',
    age: 25
};

Object.entries(person).forEach(value => {
    console.log(value);
})

// (2) ["firstName", "John"]
// (2) ["lastName", "Doe"]
// (2) ["age", 25]
```

**IMPORTANT!** 
>This syntax allows you to use ```forEach```, ```map```, ```filter``` and other methods meant for arrays but now available for objects.


## ECMAScript 9 - ES9

### Object Spread Operator

```js
const animals = {
    tiger: 23,
    lion: 5,
    monkey: 2
}

const {tiger, ...rest} = animals;

// animals
// {tiger: 23, lion: 5, monkey: 2}

// tiger
// 23

// rest
// {lion: 5, monkey: 2}
```

Or

```js
function objectSpread(p1,p2,p3) {
    console.log(p1);
    console.log(p2);
    console.log(p3);
    }

const animals = {
    tiger: 23,
    lion: 5,
    monkey: 2,
    bird: 7
}

const {tiger, lion, ...rest} = animals;

objectSpread(tiger, lion, rest);

// 23
// 5
// {monkey: 2, bird: 7}
```

### ```finally()``` 

[Go to explanation in line around 4000](####```.finally()```)

### ```for await...of```

The ```for await...of``` statement creates a loop iterating over async iterable objects as well as on sync iterables

```js
const urls = [
    "https://jsonplaceholder.typicode.com/users",
    "https://jsonplaceholder.typicode.com/posts",
    "https://jsonplaceholder.typicode.com/albums"
]

const getData = async function() {
    const arrayOfPromises = urls.map(url => fetch(url));
    for await (let request of arrayOfPromises) {
        const data = await request.json()
        console.log(data);
    }
}
```


## ECMAScript 10 - ES10

### flat() method

Method available for arrays. The ```flat()``` method creates a new array with all sub-array elements concatenated into it recursively up to the specified depth.

**Syntax**

```js
var newArray = arr.flat([depth]);
```
Default ```depth``` is ```1```

_Example:_ 

```js
const arr1 = [0, 1, 2, [3, 4]];

console.log(arr1.flat());
// expected output: [0, 1, 2, 3, 4]

const arr2 = [0, 1, 2, [[[3, 4]]]];

console.log(arr2.flat(2));
// expected output: [0, 1, 2, [3, 4]]
```

Other _Example:_

```js
const entries = ['Bob', 'Sally',,,,,, 'kevin'];
entries.flat()

//(3) ["Bob", "Sally", "kevin"]
```

### flatMap() method

Method available for arrays. The ```flatMap()``` method first maps each element using a mapping function, then flattens the result into a new array. It is identical to a ```map()``` followed by a ```flat()``` of depth ```1```, but ```flatMap()``` is often quite useful, as merging both into one method is slightly more efficient. It first ```map()``` and then it ```flat()```.

```flatMap``` only flattens 1 level deep. With ```flat()```, it accepts a parameter where you set the depth. What this means is you can specify how deep a nested array should be flattened. Now for ```flatMap()```, you can only go 1-level deep.

**Syntax**

```js
var new_array = arr.flatMap(function callback(currentValue[, index[, array]]) {
    // return element for new_array
}[, thisArg])
```

* ```callback```: Function that produces an element of the new Array, taking three arguments:
    1. ```currentValue```: The current element being processed in the array.
    
    2. ```indexOptional```: The index of the current element being processed in the array.

    3. ```arrayOptional```: The array ```map``` was called upon.

* ```thisArgOptional```: Value to use as ```this``` when executing ```callback```.

### trimStart() method

The ```trimStart()``` method removes whitespace from the beginning of a string. ```trimLeft()``` is an alias of this method.

**Syntax**

```js
str.trimStart();
str.trimLeft();
```

_Example:_

```js
const greeting = '   Hello world!   ';

console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trimStart());
// expected output: "Hello world!   ";
```

### trimEnd() method

The ```trimEnd()``` method removes whitespace from the end of a string. ```trimRight()``` is an alias of this method.

**Syntax**

```js
str.trimEnd();
str.trimRight();
```

_Example:_

```js
const greeting = '   Hello world!   ';

console.log(greeting);
// expected output: "   Hello world!   ";

console.log(greeting.trimEnd());
// expected output: "   Hello world!";
```

### fromEntries() method

The ```Object.fromEntries()``` method transforms a list of key-value pairs into an object.

**Syntax**:

```js
Object.fromEntries(iterable);
```

```iterable```: An iterable such as Array or Map or other objects implementing the iterable protocol.


_Example:_

```js
const userProfile = [['commanderTom', 23], ['derekZlander', 40], ['Hanseld', 18]]

Object.fromEntries(userProfile)

// {commanderTom: 23, derekZlander: 40, Hanseld: 18}
```

**IMPORTANT!**
>```Object.entries(object)``` does the reverse task. It turns an object, into a key-value array.

Examples: 

**Converting a Map to an Object**

With ```Object.fromEntries```, you can convert from Map to Object:

```js
const map = new Map([ ['foo', 'bar'], ['baz', 42] ]);
const obj = Object.fromEntries(map);
console.log(obj); // { foo: "bar", baz: 42 }
```

**Converting an Array to an Object**

With ```Object.fromEntries```, you can convert from Array to Object:

```js
const arr = [ ['0', 'a'], ['1', 'b'], ['2', 'c'] ];
const obj = Object.fromEntries(arr);
console.log(obj); // { 0: "a", 1: "b", 2: "c" }
```

### try...catch method

[try...catch](https://javascript.info/try-catch)

Usually, a script “dies” (immediately stops) in case of an error, printing it to console.

But there’s a syntax construct ```try...catch``` that allows us to “catch” errors so the script can, instead of dying, do something more reasonable.

The “try…catch” syntax
The ```try...catch``` construct has two main blocks: try, and then catch:

```js
try {

  // code...

} catch (err) {

  // error handling

}
```

It works like this:

1. First, the code in ```try {...}``` is executed.
2. If there were no errors, then ```catch(err)``` is ignored: the execution reaches the end of ```try``` and goes on, skipping ```catch```.
3. If an error occurs, then the ```try``` execution is stopped, and control flows to the beginning of ```catch(err)```. The ```err``` variable (we can use any name for it) will contain an error object with details about what happened.

So, an error inside the ```try {…}``` block does not kill the script – we have a chance to handle it in catch


_Example:_

```js
try {

  alert('Start of try runs');  // (1) <--

  lalala; // error, variable is not defined!

  alert('End of try (never reached)');  // (2)

} catch(err) {

  alert(`Error has occurred!`); // (3) <--

}
```

## Advanced Loops

Traditional way of looping:

```js
const basket = ['apples', 'oranges', 'grapes'];

//1

for (let i = 0; i < basket.length; i++) {
    console.log(basket[i]);
}

// 2

basket.forEach(item => {
    console.log(item);
})
```

____

**IMPORTANT!**
[Enumerables - Iterators / for...of y for...in](https://medium.com/better-programming/what-is-the-difference-between-for-in-and-for-of-in-javascript-650952654e97)
____

_Additional Note:_
>Iterable: ordered;
>Enumerables: are unorder;

[for... of and for...in](https://reactgo.com/javascript-for-of-vs-for-in-loop/)

### ```for...of``` 

Use ```for…of``` to iterate over the values in an iterable (ordered), like an array for example. An iterable is required after the ```of``` keyword — in contrast to the requirement of an enumerable with ```in```. It's mainly applied on strings and arrays given that they are _iterables_. 

```js
let str = 'abcde';

for (let char of str) {
  console.log(char.toUpperCase().repeat(3));
}

// AAA
// BBB
// ...
```

### ```for...in```

We begin with ```for...in```, which is used to loop over an **enumerable** (unorder). This is perfect for counting over key-value pairs in an object, such as the example below. It's mainly applied on objects. 

```js
let person = {
   "first_name": "Jonathan",
   "last_name": "Hsu",
   "medium-handle": "@jhsu98"
}
for(const key in person) {
   console.log(key + ": " + person[key]);
}
/*
"first_name: Jonathan"
"last_name: Hsu"
"medium-handle: @jhsu98"
*/
```

As you can see, the ```for...in``` loop will set the temporary variable to each key of the object. Therefore, in this case, what is being counted over are the identifiers.

**Access object properties (keys)**

Use ```for…in``` to iterate over the properties of an object (the object keys):

```js
let oldCar = {
  make: 'Toyota',
  model: 'Tercel',
  year: '1996'
};

for (let key in oldCar) {
  console.log(`${key} --> ${oldCar[key]}`);
}

// make --> Toyota
// model --> Tercel
```

**Access object values instead of keys**

Let’s see how to access the object values instead of keys.

```js
const obj = {
    a:1,
    b:2,
    c:3
}

for(let key in obj){
    console.log(obj[key]);
}

//output

//first iteration: 1
//second iteration : 2
//third iteration : 3
```

You can also use ```for…in``` to iterate over the index values of an iterable like an array or a string:

```js
let str = 'Turn the page';

for (let index in str) {
  console.log(`Index of ${str[index]}: ${index}`);
}

// Index of T: 0
// Index of u: 1
```

**IMPORTANT!**
>I Thought Arrays Were Enumerables Too
>You’re right! We saw that passing an enumerable to ```for...of``` will cause an error, but passing an iterable to ```for...in``` is accepted.
>Similar to how ```for...in``` counts over the identifiers of the object, ```for...in``` will count over the indexes — think of them as position identifiers.


## Debugging 

```js
const flattened = [[0,1], [2,3], [4,5]].reduce(
    (a,b) => a.concat(b), []);
```

**1st step**

Traduce de code into something you can understund:

```js
const flattened = [[0,1], [2,3], [4,5]].reduce(
    (accumulator, array) => {
        console.log('array', array); 
        console.log('accumulator', accumulator); 
        return accumulator.concat(array)
    }, []);

// array (2) [0, 1]
// accumulator []
// array (2) [2, 3]
// accumulator (2) [0, 1]
// array (2) [4, 5]
// accumulator (4) [0, 1, 2, 3]
```

**2nd step** 

Implement ```debugger```. When the JavaScript engine runs into the key word ```debugger```, the code stops there and opens up a debugging window exactly where the code ran into the ```debugger``` word. At this point you can:

* **Press play**

* **Step over:** runs a line and stops again until you step over again and so on

```js
const flattened = [[0,1], [2,3], [4,5]].reduce(
    (accumulator, array) => {
        debugger;
        return accumulator.concat(array)
    }, []);

```

## How JavaScript Works

1. **Browser Engine** reads the javascript that we write. This engine, consists on two parts:
    
    * **Memory Heap**: is where the memory allocation happens. I.e: ```const a = 1;``` gets stored in memory heap. When you have unused memory, like storing variables that you aren't actually using, **memory leaks** happen, given that the memory heap fills up. For this, **you might hear that global variables are bad because if you forget to clean them up, you can fill up the memory heap**. When the stack is overflowed, memory leak happens.

    * **Call Stack**: is where the code is read and executed. It tells you where you are in the program. El _call stack_ es la "pila" donde se van almacenando las ordenes de ejecucion que indica el codigo. Si le digo que ejecute un ```console.log()```, eso se va al call stack, se ejecuta, y luego se popea del call stack. Luego, se ejecuta la proxima tarea que se presente segun lo que indica el código. It follows the idea of _first in, last out_
    ```js
    const one = () => {
        const two = () => {
            console.log('4');
        }
        two();
    }
    one()
    ```
    This is the call stack working:
    
    1st to enter: ```const one = () =>``` 
    2nd to enter: ```const two = () =>``` 
    3nd to enter: ```console.log('4')``` 
    <--------------------------------->
    1st to go out: ```console.log('4')```
    2nd to go out: ```const two = () =>``` 
    3rd to go out: ```const one = () =>```
    <--------------------------------->
            Call Stack Empty

**JavaScript is a single threaded language that can be non-blocking**

* _Single threaded_: means that JS has only one _call stack_, for what you can just do one thing at a time. Call stack is first in, last out, so whatever is at the top of the call stack gets run first and then below that until the call stack is empty. Others languages can have multiple call stacks, for that they are acalled **multi thread langauges**. 

[Non-Blocking](https://medium.com/javascript-in-plain-english/js-single-thread-non-blocking-explained-d5de012a33cf)

* _non-blocking_: Non-blocking refers to code that doesn't block execution. Non-blocking is effectively the same as asynchronous - you make the call, and you'll get a result later, but while that's happening you can do something else. Blocking is the opposite. You wait for the call to return before you continue your journey.


**Synchronous vs Asynchronous**:

* **Synchronous** basically means that you can only execute one thing at a time. **Asynchronous** means that you can execute multiple things at a time and you don't have to finish executing the current thing in order to move on to next one.

_Additional Note:_
[Recursion - for noobs](https://www.freecodecamp.org/news/quick-intro-to-recursion/)
>**Recursion**: Recursion is when a function calls itself until someone stops it. If no one stops it then it'll recurse (call itself) forever. Recursion is a programming term that means calling a function from itself. Recursive functions can be used to solve tasks in elegant ways. When a function calls itself, that’s called a recursion step. The basis of recursion is function arguments that make the task so simple that the function does not make further calls. 
>Recursive functions let you perform a unit of work multiple times. This is exactly what for/while loops let us accomplish! Sometimes, however, recursive solutions are a more elegant approach to solving a problem.

### Asynchronous programming

[Asynchronous - Andrei Neagoie](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/9427570#announcements)

```setTimeout()``` is a function that comes within the browser:
1. First parameter is the function that we want to run.
2. Secon parameter is the milisecond we wanna wait

```js
console.log('1');
setTimeout(() => { 
    console.log('2');
}, 2000)
console.log('3');

// 1
// 3
// undefined
// 2
```

In order for JavaScript to run for the JS engine with the memory heap and call stack, we need more than the JavaScript engine. **For that, we need what we call a _JavaScript Run-Time Environment_, which is part of the browser**. This environment has extra engine:

* Web API'S
    1. Timeout (```setTimeout```): is part of the browser environment, so we can do asynchronous programming. 
* Callback Queue
* Event Loop

**When the browser's ```setTimeout``` function is called and detected, that task is "sent" to the Web API. And because it's not using the Call Stack, JavaScript can read the next line given that it has "space" in the call stack to do so. Meanwhile, when the timeout pass, the task is sent to callback queue, meaning that it's ready to run. Also, the Event Loop checks if the call stack is empty; and if it is, is going to check in the callback if there is anything in queue. If there is, that task is sent to the call stack.** 

```js
console.log('1');
setTimeout(() => { 
    console.log('2');
}, 2000)
console.log('3');

// CALL STACK

// WEB API

// CALLBACK QUEUE

// EVENT LOOP
```

### Modules

[Modules - Andrei Neagoie](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8691796#announcements)

[About Module usage](https://exploringjs.com/es6/ch_modules.html)

[History of JavaScript Modules](https://medium.com/sungthecoder/javascript-module-module-loader-module-bundler-es6-module-confused-yet-6343510e7bde)

Browserify is a module bundler. It runs before you put the website on line; it reads through al lthe javascript files, reads through all the syntax, and it bundles everything into a single file. All this issue was born because JavaScript didn't have a module system built into de language. 

But with ES6, that changed. It brought to new components:

1. ```export```
2. ```import```

```js
// js1
export const add = (a, b) => a + b; // with this you can export multiple functions in the same file

// or

export default function add() {     // with this you can export only one thing
    return a + b; 
}

// js2

import { add } from './add'; // ----> destructuring

// or

import add from './add';
```

Not all browsers do support this new ES6 new feature. For this, Webpack2 was created.

#### Webpack2

Webpack is a static module bundler for JavaScript applications — it takes all the code from your application and makes it usable in a web browser. Modules are reusable chunks of code built from your app’s JavaScript, node_modules, images, and the CSS styles which are packaged to be easily used in your website. Webpack separates the code based on how it is used in your app, and with this modular breakdown of responsibilities, it becomes much easier to manage, debug, verify, and test your code.

With Webpack, we can actually use ES6 in all browsers. 

//webpack

```js
module.exports = {
    entry: './app/main.js',
    output: {
        path: './dist',
        filename: 'bundle.js'
    }
}
```


## Git SSH set-up

[Git SSH set-up by Andrei Neagoie](https://www.udemy.com/course/complete-react-developer-zero-to-mastery/learn/lecture/15359990#questions)

## Git Bash

```bash
ls
pwd
cd 
cd ..
clear
cd / **—> root director**
cd ~
cd <folder/folder/folder> ** <> means to add your own folder names that exist on your computer.
mkdir <folder>
open <folder> **for windows use: start <folder>
touch index.html  **for windows use: echo "" > index.html
open index.html **for windows use: start index.html
open -a “Sublime Text”  **for windows see the note about this at the bottom of this lecture!!
open . **for windows use: start .
mv index.html about.html
*Try using the Up and Down arrow.
 
rm <file>
rm -r <folder>
say hello **(only on Mac)**
```

* **oh my ZSH** an alternative to bash


# NPM & NPM Scripts

[NPM JavaScript Package Downloaders](https://www.npmjs.com/)

NPM, for Node Package Manager, was created fot the developers to share JavaScript code that they have written.

Each module, contains a javascript file and a JSON file, which is a meta file that describes the package. 

There is usually three types of packages:

1. Packages to use on the frontend, like JQuery. 

2. Packages that give you new commands that you can use in the command line. 

3. Packages to use in the backend, like Node.js

## Node.js 

Allows us to run JavaScript outside of the browser. Node.js was created actually using the V8 engine from Google Chrome, to read and run JavaScript outside of the browser. Node.js automatically installs NPM.

To check version write ```node -v``` and ```npm -v``` in CLI.

**Every time you start a project, you want to creat the NPM JSON file by typing in the command line, inside the folder that correspondes, ```npm init```**


### Live-server, React and loadash

* ```npm install -g live-server```: - the ```g``` stands for globaly, which means you can run it anywhere, not only in one project, including your terminal. If you don't install it globaly, you want be able to run it from your terminal. To run live-server, type ```live-server``` in the command line, inside the folder you wish to run on live-server.

```npm i --save lodash```: to install locally, you can do ```npm install lodash```

### Installing modules from package.json

Type ```npm install``` inside the folder where the package.json exists. 

# React

React is a view library. React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components”.

* The idea of React is that data flows from top to bottom (one-way data flow principle). So, if a component has children and that component changes, then only the children are "affected" by their parent-component change, because the direction of the data flow is only downstream. 

![One-way data flow principle](https://miro.medium.com/max/550/1*PBgAz9U9SrkINPo-n5glgw.gif)


* The idea of **Virtual DOM**. Remember that the idea is to minimize the amount of DOM manipulation we do, because it affects the performance of the web page and increases the risk of bugs. React creates a Virtual DOM, which is a JavaScript object that describes the current state of the website. We give that object to React, and the React Engine will automatically make changes to the DOM in the most optimum way possible. 

* React Ecosystem

## Robofriends

[What create-react-app does for us behind the sceens](https://www.udemy.com/course/complete-react-developer-zero-to-mastery/learn/lecture/14915222#questions)

1. ```npm install -g create-react-app``` ---> nowadays we can better use ```npx create-react-app nameofapphere```, which is a package runner tool that comes with npm. 


2. ```create-react-app robofriends```

3. ```npm start```

```package-lock.json``` is automatically created by ```package.json``` to make sure that the version number of the dependencies are locked in. 

_Additional Note:_
>**Updating libraries version like ```create-react-app```**: go to ```package.json```, find ```    "react-scripts": "3.4.3"```, update the numbers for the version following the latest one, and then run in the CLI ```npm install``` and that will upgrade the version of the package. 

## index.js

* ```import React from 'react';```: this is the view generic library

* ```import ReactDOM from 'react-dom';```: this is the library to use react for web design purposes. If you were to build mobile apps, you would use ```react-native```, as example.

* ```import './index.css';```: this will apply style to whatever components we have at ```index.html``` 

* ```import * as serviceWorker from './serviceWorker';```: allows apps to become faster and potentially work off-line. 

* 
```js
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
**This means: I want ```ReactDOM``` package to ```render``` whatever the argument is.**

* You can do:

```js
import React from 'react';
class App extends React.Component {...}
```
or
```js
import React { Component } from 'react';
class App extends Component {...}
```

* A ```Component``` is always followed by a ```render()``` function because it must always render something:

The ```render``` method returns a description of what you want to see on the screen. React takes the description and displays the result. In particular, ```render``` returns a React element, which is a lightweight description of what to render. Most React developers use a special syntax called “JSX” which makes these structures easier to write. The ```<div />``` syntax is transformed at build time to ```React.createElement('div')```

_Example:_


```js
class App extends Component {
    render() {
        return (
            // html here
        );
    }
}
```

* export default meaning

When creating a component, we need to export it to be able to render it and to be used by another file. Else, an error like ```export 'default' was not found in './module'```.

**We use ```export default``` when we are just exporting one thing from that file. If we were to use more than one element from the same file, we would just ```export``` the element, like ```export const robots```. For those that are no ```export default```, you have to destructure it when importing the element: ``` import { robots } from './robots'```**

```js
import React, { Component } from 'react';

class Hello extends Component {
    render() {
        return <h1>Hello World</h1>
    }
}

export default Hello;
```

If we do something like the following snippet, it won't work, because ```return``` expects a single thing.
To fix that, we need to wrap the snippet in parenthesis, in order to JavaScript realize that it's an expression and must evaluate the entire snippet. 

```js
import React, { Component } from 'react';

class Hello extends Component {
    render() {
        return 
        <div>
            <h1>Hello World</h1>
            <p>Welcome to React!</p>
        </div>
    }
}

export default Hello;
```

Fixed issue:

```js
import React, { Component } from 'react';

class Hello extends Component {
    render() {
        return (
        <div>
            <h1>Hello World</h1>
            <p>Welcome to React!</p>
        </div>
        );
    }
}

export default Hello;
```

* Creating and importing a ```Hello.css``` file

```import './Hello.css';``` this line must go in the ```Hello.js``` file, which will take all the styling code from the css file to style the component. 


### Tachyons

Similar to Bootstrap, allows us to have classes that we can add to components. 

```npm install tachyons```

```import 'tachyons';``` at ```index.js```

You can style with tachyons by adding the elements to a ```className``` like the following:

```js
<div className="f1 tc">
    <h1>Hello World</h1>
    <p>Welcome to React!</p>
</div>
```

We can't use ```class``` because it is a reserved word for JavaScript language; instead, we use ```className```. And eventhough it looks like HTML, it is JSX. 

This syntax is actually called **JSX**. Underneath the hood what React is doing through JSX is letting us use this syntax (```<div className="f1 tc">```) that looks like HTML but is not actually HTML. For this, React uses **JSX** to create their Virtual DOM. **React compares the Real DOM vs. the Virtual DOM and makes the changes that which must be done only**.

[Separation of concerns](https://medium.com/@alialhaddad/separation-of-concerns-in-react-d4f74aaf3800)

_Additional Note:_
> JSX: JSX is an XML/HTML-like syntax used by React that extends ECMAScript so that XML/HTML-like text can co-exist with JavaScript/React code. The syntax is intended to be used by preprocessors (i.e., transpilers like Babel) to transform HTML-like text found in JavaScript files into standard JavaScript objects that a JavaScript engine will parse.

>Basically, by using JSX you can write concise HTML/XML-like structures (e.g., DOM like tree structures) in the same file as you write JavaScript code, then Babel will transform these expressions into actual JavaScript code. Unlike the past, instead of putting JavaScript into HTML, JSX allows us to put HTML into JavaScript.

## Adding props / properties to components

Within a component, I can add properties to it.

A component takes in parameters, called ```props``` (short for “properties”), and returns a hierarchy of views to display via the render method.

```js
ReactDOM.render(
  <React.StrictMode>
    <Hello greeting={'Hello' + 'React Ninja'} />
  </React.StrictMode>,
  document.getElementById('root')
);
```

Now, I have access to the ```props``` greeting from my ```Hello.js``` component:

```js
return (
<div className="f1 tc">
    <h1>Hello World</h1>
    <p>{this.props.greeting}</p>
</div>
);
```

With this syntax I'm saying that ```this``` object ```Hello``` has properties ```props``` that is ```greeting```.

## Moving from class components to functions components

Instead of using classes to instantiate components, we can, and should, functions. For that, we are going to change our ```Hello``` component from ```Hello.js``` from this:

```js
class Hello extends Component {
    render() {
        return (
        <div>
            <h1>Hello World</h1>
            <p>Welcome to React!</p>
        </div>
        );
    }
}
```
To this:

```js
const Hello = (props) => {
    return (
        <div className="f1 tc">
            <h1>Hello World</h1>
            <p>{props.greeting}</p>
        </div>
    );
}
```

**Among other changes, ```this``` is erased, because ```Hello``` is not a class anymore, meaning, it's not an object anymore but a function. And this functions, take parameters that are given by giving attributes and values are just being rendered** 

## ```<div>``` vs <> - ```<div>``` vs Fragment

[React.Fragment to avoid ```<div>```](https://blog.logrocket.com/rendering-sibling-elements-react-fragments/)

## Importing Robots Information

We have a list full of objects that contains the information for the cards that will be in each robot. 

That information is being held at ```robots.js```, in a list, which contains objects inside. If we want to export more than one element from the same file, we just ```export const robots```; else, we use ```export default cons robots```. But this is not the case. 

Also, to import that list into ```index.js```, and considering we just ```export``` the element, we have to import it at ```index.js``` by destructuring: ```import { robots } from './robots'```; if you had to import more than one element, you would destructure like this: ```import { robotos, cats } from './robots'```; otherwise, if it was an ```export default``` we would just do ```import robots from './robots'```


_Remember:_
>**We use ```export default``` when we are just exporting one thing from that file. If we were to use more than one element from the same file, we would just ```export``` the element, like ```export const robots```. For those that are no ```export default```, you have to destructure it when importing the element: ```import { robots } from './robots'```**

### Robots properties

To add the properties to the robots card, you can do something like this at ```index.js```:

```js
ReactDOM.render(
  <React.StrictMode>
  <div>
    <Card id={robots[0].id} name={robots[0].name} email={robots[0].email} />
    <Card id={robots[1].id} name={robots[1].name} email={robots[1].email} />
    <Card id={robots[2].id} name={robots[2].name} email={robots[2].email} />
  </div>
  </React.StrictMode>,
  document.getElementById('root')
);
```

And then add this to ```Card.js```:

```js
import React from 'react';

const Card = (props) => {
    return (
        <div className="bg-light-green dib br3 pa3 ma2 grow bw2 shadow-5">
            <img src="https://robohash.org/test?size=200x200" alt="robots"/> 
            <div>
                <h2>{props.name}</h2>
                <p>{props.email}</p>
            </div>
        </div>
    );
}

export default Card;
```

We pass the argument ```props``` to the function and then, inside curly brackets we assign the properties. 

**IMPORTANT!**
*By wrapping expressions in curly brackets, we "transform" them from JSX to pure JavaScript*.


#### Destructure the argument ```props```

To avoid calling the property like we regularly do (```props.attribute```), we can destructure the ```props``` variable:

```js
import React from 'react';

const Card = ({ name, email, id }) => {
    return (
        <div className="tc bg-light-green dib br3 pa3 ma2 grow bw2 shadow-5">
            <img src={`https://robohash.org/${id}?size=200x200`} alt="robots"/> 
            <div>
                <h2>{name}</h2>
                <p>{email}</p>
            </div>
        </div>
    );
}

export default Card;
```

### Creating a CardArray

1. First of all, change ```index.js```. As we are going to add multiple cards, we will do it through an array, instead of copying and pasting each card a bunch of times.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import CardList from './CardList'; //<----------- Also import this component that will be used later
import * as serviceWorker from './serviceWorker';
import 'tachyons';
import { robots } from './robots';

ReactDOM.render(
  <React.StrictMode>
    <CardList robots={robots} /> //<------------- Here we add the attribute {robots}, which is imported.
  </React.StrictMode>,
  document.getElementById('root')
);
```

1. Create a ```CardList.js```. Generate a function that takes the ```props``` ```robots``` and inside create a function that loops through all the ```robots``` array that returns a new array called ```cardComponent``` with the information of each robot and whcih is returned as a component, which is later exported as default. 

```js
import React from 'react';
import Card from './Card';

const CardList = ({ robots }) => {
    const cardComponent = robots.map((user, i) => {
        return <Card id={robots[i].id} name={robots[i].name} email={robots[i].email} /> 
    })
    return (
      <div>
        {cardComponent}
      </div>
    
    );
}

export default CardList;
```


#### Console Warning

```js
index.js:1 Warning: Each child in a list should have a unique "key" prop.

Check the render method of `CardList`. See https://fb.me/react-warning-keys for more information.
    in Card (at CardList.js:6)
    in CardList (at src/index.js:11)
    in StrictMode (at src/index.js:10)
```

**When working with React the way the Virtual DOM works is to keep track of what all the cards are. But without having a ```key``` prop, if some of the cards get deleted, React won't know which one is which and will have to change the entire DOM versus if it has a ```key``` prop, where it would be able to detect which one was removed. So, when you loop, you have to give the element a unique ```key```** See below:

In ```CardList.js```

```js
const CardList = ({ robots }) => {
    const cardComponent = robots.map((user, i) => {
        return <Card key= {i} id={robots[i].id} name={robots[i].name} email={robots[i].email} /> 
    })
    return (
      <div>
        {cardComponent}
      </div>
    
    );
}
```

### Adding the App parent component

Once you start building more and more components, is a good practice to create and ```App``` module that is the parent of all the other components. Thus, at the end of the way you can just ```import App from './App'``` instead of importing each component separately from their own file.  

```js
import React from 'react';
import CardList from './CardList';
import SearchBox from './SearchBox';
import { robots } from './robots';

const App = () => {
    return (
        <div className="tc">
            <h1>Robofriends</h1>
            <SearchBox />
            <CardList robots={robots} />
        </div>
    );
}

export default App;
```

### SearchBox

In order to connect the SerachBox to the CardList, they need to communicate. How? Through **states**

#### State Managment

To “remember” things, components use state. React components can have state by setting ```this.state``` in their constructors. ```this.state``` should be considered as private to a React component that it’s defined in

A state is something that can change and affect our App. It means the description of your App. They usually live in the parent component, which passes a state, to different components. 
Is an object that describes our application. This state in this case is the robots and whatever is entered in the SearchBox. **And state is able to change**: we are able to change the avalue of the input value of the SearchBox, and we are able to change what robots get displayed. ```props``` are simply things that come out of ```states```. So, **a parent feeds a state into a child component and as soon as the child component receives the state, it becomes a property; that child can never change that property. The parent just tells it what the state is and the child just receives it as "robots"**

In order tu use states, we have to go to the original way in which we created components. 

So, from this: 

```js
import React from 'react';
import CardList from './CardList';
import SearchBox from './SearchBox';
import { robots } from './robots';

const state = {
    robots: 'robots',
    searchField: ''
}

const App = () => {
    return (
        <div className="tc">
            <h1>Robofriends</h1>
            <SearchBox />
            <CardList robots={robots} />
        </div>
    );
}

export default App;
```

We move to this: 

```js
import React, { Component } from 'react';
import CardList from './CardList';
import SearchBox from './SearchBox';
import { robots } from './robots';

class App extends Component {
    constructor() {
        super()
        this.state = {
            robots: robots,
            searchField: ''
        }
    }
    render() {
        return (
            <div className="tc">
                <h1>Robofriends</h1>
                <SearchBox />
                <CardList robots={this.state.robots} />
            </div>
        );
    
    }
}

export default App;
```

[Handling Events with React](https://reactjs.org/docs/handling-events.html)

[Udemy Video to understund this section](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8757618?start=825#questions)

_Additional Note:_
>We use ```this.state.robots``` or ```this.onSearchChange``` because we refer to the ```App``` object, where ```this.state``` is a property of that object. 

#### event.target.value

```event.target.value``` allows us to access the value that is actually being inserted in the ```input``` box. This is usefull fo the ```SearchBox``` component. 


![One-way data flow - React](https://miro.medium.com/max/550/1*PBgAz9U9SrkINPo-n5glgw.gif)


[One-way data flow vs Redux](https://medium.com/@alialhaddad/https-medium-com-alialhaddad-redux-vs-parent-to-child-2583c8e29509)



#### SearchBox filtering input

Up to this point, we would have this code in ```App.js```:

```js
import React, { Component } from 'react';
import CardList from './CardList';
import SearchBox from './SearchBox';
import { robots } from './robots';

class App extends Component {
    constructor() {
        super()
        this.state = {
            robots: robots,
            searchfield: ''
        }
    }

    onSearchChange = (event) => {
        const filteredRobots = this.state.robots.filter(robot => {
            return robots.name.toLowerCase().includes(this.state.searchfield.toLowerCase());
        })
        console.log(filteredRobots);
    }

    render() {
        return (
            <div className="tc">
                <h1>Robofriends</h1>
                <SearchBox searchChange = {this.onSearchChange}/>
                <CardList robots={this.state.robots} />
            </div>
        );
    
    }
}

export default App;
```

**IMPORTANT!**

The following snippet is meant to filter only the robots that match whatever is inside the ```SearchBox``` input:

```js
    onSearchChange = (event) => {
        const filteredRobots = this.state.robots.filter(robot => {
            return robots.name.toLowerCase().includes(this.state.searchfield.toLowerCase());
        })
        console.log(filteredRobots);
    }
```

**IMPORTANT!**

**We use ```onSearchChange = (event) =>``` instead of ```onSearchChange(event) { ... }``` because otherwise that app would crash. Why? Because here:**

```js
{
        const filteredRobots = this.state.robots.filter(robot => {
            return robots.name.toLowerCase().includes(this.state.searchfield.toLowerCase());
        })
        console.log(filteredRobots);
    }
```

**the value of ```this``` is not referring to the ```App```, because the ```event``` is happening in the input, the value of ```this``` is the input, and the input doesn't have ```state.robots```, thus, we hack it by using ```onSearchChange = (event) =>``` instead of ```onSearchChange(event) { ... }```**. Why? **because with anything that comes from ```React```, like ```constructor()``` or ```rener()``` which are pre-built in ```React```, any time you make your own methods on a component use the arrow function syntax: ```onSearchChange = (event) =>```.That way, you make sure that the value of ```this``` is according to where it was created, in this case, the ```App```**

#### Updating searchfield state

Up until this point, we are filtering information but the ```searchfield``` state is not being updated. To do that, we use a method that comes with React which is ```setState()```

```js
this.setState({ searchfield: event.target.value })
```

This way, the ```onSearchChange``` function would look something like this:

```js
onSearchChange = (event) => {
    this.setState({ searchfield: event.target.value })
    const filteredRobots = this.state.robots.filter(robots => {
        return robots.name.toLowerCase().includes(this.state.searchfield.toLowerCase());
    })
}
```

**IMPORTANT!**

[```setState``` React Doc](https://reactjs.org/docs/faq-state.html#what-does-setstate-do)

**What does ```setState``` do?**

>```setState()``` schedules an update to a component’s state object. When state changes, the component responds by re-rendering.

**Why is ```setState``` giving me the wrong value?**
>Calls to ```setState``` are asynchronous - don’t rely on ```this.state``` to reflect the new value immediately after calling ```setState```. Pass an updater function instead of an object if you need to compute values based on the current state.

**How do I update state with values that depend on the current state?**

>Pass a function instead of an object to ```setState``` to ensure the call always uses the most updated version of state (see below).

**What is the difference between passing an object or a function in ```setState```?**

>Passing an update function allows you to access the current state value inside the updater. Since ```setState``` calls are batched, this lets you chain updates and ensure they build on top of each other instead of conflicting:

```js
incrementCount() {
  this.setState((state) => {
    // Important: read `state` instead of `this.state` when updating.
    return {count: state.count + 1}
  });
}

handleSomething() {
  // Let's say `this.state.count` starts at 0.
  this.incrementCount();
  this.incrementCount();
  this.incrementCount();

  // If you read `this.state.count` now, it would still be 0.
  // But when React re-renders the component, it will be 3.
}
```
____

**IMPORTANT!**

DOM Events for React!!! Called ```SyntheticEvent```

[Events](https://reactjs.org/docs/events.html#clipboard-events)

____

#### Binding this to the App context

[To expand on binding and arrow functions go here](https://www.udemy.com/course/complete-react-developer-zero-to-mastery/learn/lecture/14870617#questions)

**IMPORTANT!**

**For class components with constructor and state:** Before starting, ES6 and arrow functions allows us to set the context of ```this``` in whatever was that declared it in the first place. So, arrow functions allow us to automatically set ```this``` when the arrow function is defined:

```js
handleChange = (e) => {
    this.setState({ searchField: e.target.value})
}
```

They autimatically get what is called lexical scoping, which means that they bind the ```this``` context to the place where they were defined in the first place.

A good rule of thumb is this: **Use arrow functions on any class methods you define and aren't part of React (i.e. ```render()```, ```componentDidMount()```).**

When you define a component using an ES6 class, a common pattern is for an event handler to be a method on the class. For example, this Toggle component renders a button that lets the user toggle between “ON” and “OFF” states:

```js
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);// <-------
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>           // <-------
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

You have to be careful about the meaning of ```this``` in JSX callbacks. In JavaScript, class methods are not bound by default. If you forget to bind ```this.handleClick``` and pass it to onClick, ```this``` will be ```undefined``` when the function is actually called.

This is not React-specific behavior; it is a part of how functions work in JavaScript. Generally, if you refer to a method without ```()``` after it, such as ```onClick={this.handleClick}```, you should ```bind``` that method.

If calling ```bind``` annoys you, there are two ways you can get around this. If you are using the experimental public class fields syntax, you can use class fields to correctly ```bind``` callbacks:

```js
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

This syntax is enabled by default in Create React App.

If you aren’t using class fields syntax, you can use an arrow function in the callback:

```js
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // This syntax ensures `this` is bound within handleClick
    return (
      <button onClick={() => this.handleClick()}>
        Click me
      </button>
    );
  }
}
```

The problem with this syntax is that a different callback is created each time the ```LoggingButton``` renders. In most cases, this is fine. However, if this callback is passed as a prop to lower components, those components might do an extra re-rendering. We generally recommend binding in the constructor or using the class fields syntax, to avoid this sort of performance problem.

#### Connecting searchfield state with CardList

For that, we would change the following snippet:

```js
    onSearchChange = (event) => {
        this.setState({ searchfield: event.target.value })
        const filteredRobots = this.state.robots.filter(robots => {
            return robots.name.toLowerCase().includes(this.state.searchfield.toLowerCase());
        })
    }

    render() {
        return (
            <div className="tc">
                <h1>Robofriends</h1>
                <SearchBox searchChange = {this.onSearchChange}/>
                <CardList robots={this.state.robots} />
            </div>
        );
    
    }
```

to this one:

```js
    onSearchChange = (event) => {
        this.setState({ searchfield: event.target.value })
    }

    render() {
        const filteredRobots = this.state.robots.filter(robots => {
            return robots.name.toLowerCase().includes(this.state.searchfield.toLowerCase());
        })
        return (
            <div className="tc">
                <h1>Robofriends</h1>
                <SearchBox searchChange = {this.onSearchChange}/>
                <CardList robots={filteredRobots} />
            </div>
        );
    
    }
```

The constant ```filteredRobots``` is moved to the ```render()``` pre-built function. And the ```<CardList robots={this.state.robots} />``` is changed to ```<CardList robots={filteredRobots} />```; this way, the only card that gets rendered is the one that is getting filtered by the attribute ```robots```.


#### Smart Components

Components that have ```state```, like our ```App``` class component, are called **smart components**. Smart components tend to have the ```class App extends Component``` syntax. 

In a real app, ```robots``` would most likely be using elemnts from a json stored in some server and grabbing the information from there.

#### Life-Cycle Methods

React lets you define components as classes or functions. Components defined as classes currently provide more features which are described in detail on this page. To define a React component class, you need to extend ```React.Component```:

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

The only method you must define in a ```React.Component``` subclass is called ```render()```. All the other methods described [on this page](https://reactjs.org/docs/react-component.html) are optional.

React comes with a few other things inside of the ```Components``` that we can use. They are called ```life-cycle methods```

[Life-Cycle Methods](https://reactjs.org/docs/react-component.html)

**Life-Cycle Hooks/Methods get automatically triggered when the app gets loaded on the website**.

We have three sections inside the life-cycle: 

1. *Mouting:* when we refresh the page, the ```App``` component gets mounted into the ```document.getElementById('root')``` that belongs to:

```js
ReactDOM.render(
  <React.StrictMode>
    < App />
  </React.StrictMode>,
  document.getElementById('root')
)
```

And if you go to _index.html_ you will find that the first ```<div>``` in the ```<body>``` is a ```<div id="root"></div>```.

**When we say we mount a component, we are replacing ```<div id="root"></div>``` and adding our entire ```App```. So mounting is the start of the app**

These methods are called in the following order when an instance of a component is being created and inserted into the DOM (meaning, during *Mounting*):

* ```constructor()```
* ```static getDerivedStateFromProps()```
* ```render()```
* ```componentDidMount()```

So, React checks if the Component has a ```constructor()```; if it does, ir runs tha piece of code. Then it checks if it has a ```static getDerivedStateFromProps()``` and so on. 

2. *Updating:* Updates happen whenever a component changes. Like in the robofriends app, everytime we would type something in the searchbox, the ```CardList``` we be updated and re-rendered. 

3. *Unmounting:* Unmounting happens whe a component is removed from a page. So if we change from one web app to the other, the first web app components will be unmounted or removed. 


_Additional Note:_
>What are React lifecycle methods? You can think of React lifecycle methods as the series of events that happen from the birth of a React component to its death.

>Every component in React goes through a lifecycle of events. I like to think of them as going through a cycle of birth, growth, and death.

>1. Mounting – Birth of your component
>2. Update – Growth of your component
>3. Unmount – Death of your componen

#### Fetch

JavaScript can send network requests to the server and load new information whenever it’s needed.

For example, we can use a network request to:

* Submit an order,
* Load user information,
* Receive latest updates from the server,

And all of that without reloading the page!

The basic syntax is:

```js
let promise = fetch(url, [options])
```

* ```url``` – the URL to access.
* ```options``` – optional parameters: method, headers etc.

##### POST requests with fetch

To make a ```POST``` request, or a request with another method, we need to use ```fetch``` options:

* ```method``` – HTTP-method, e.g. POST,
* ```body``` – the request body, one of:
    * a string (e.g. JSON-encoded),
    * ```FormData``` object, to submit the data as ```form/multipart```,
    * ```Blob/BufferSource``` to send binary data,
    * URLSearchParams, to submit the data in ```x-www-form-urlencoded``` encoding, rarely used.

The JSON format is used most of the time.

For example, this code submits ```user``` object as JSON:

```js
let user = {
  name: 'John',
  surname: 'Smith'
};

let response = await fetch('/article/fetch/post/user', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json;charset=utf-8'
  },
  body: JSON.stringify(user)
});

let result = await response.json();
alert(result.message);
```

Please note, if the request ```body``` is a string, then ```Content-Type``` header is set to ```text/plain;charset=UTF-8``` by default.

But, as we’re going to send JSON, we use ```headers``` option to send ```application/json``` instead, the correct Content-Type for JSON-encoded data.

#### Setting state with Fetch

To set the ```state``` of ```robots``` first of all we must instatiante the ```robots``` object property equal to an empty array; this way, we will grab information (through ```fetch```) and use ```setState``` to link that response to the ```state``` of ```robots```. Then, we use the life cycle method ```    componentDidMount()``` to throw a function right after the ```App``` component has been loaded and rendered.

```js
componentDidMount() {
    fetch('http://jsonplaceholder.typicode.com/users')
    .then(response => response.json())
    .then(users => this.setState({ robots: users }))
} 
```

How this works:

1. We fetch the users from ```jsonplaceholder```

2. We manipulate that response and transform it into a json format file for React and JS to understund it.

3. From that json we take the ```users``` and update them in ```robots``` with ```setState```.


### Scroll component

The idea is to create a container where all the Cards exist and in case you have to scroll, you just do it by scrolling that container while your ```SearchBox```, which exists outside that component, always stay on top of the app. 

#### ```this.props.children```

Some components don’t know their children ahead of time. This is especially common for components like ```Sidebar``` or ```Dialog``` that represent generic “boxes”.  It is used to display whatever you include between the opening and closing tags when invoking a component.

We recommend that such components use the special ```children``` prop to pass children elements directly into their output.

```js
import React from 'react';

const Scroll = (props) => {
    return (
        <div style={{ overflowY: 'scroll', border: '1px solid black', height: '500px' }}>
            {props.children}
        </div>
    );
};

export default Scroll;
```

### Folder structure

* _Components_ folder

* _Containers_ folder: they are they ones that passes out states to components, such as ```App.js```

```npm run build``` creates a ```build``` folder with minified documents which is ready to be deployed.

#### Updating project

```npm update```

```npm audit```

```npm audit fix```

```npm audit fix --force```

## Error Boundaries

The way React works with the virtual DOM, it waits for changes to be finished before updating it in the real DOM.

Most times, the error had occurred somewhere inside a component in your application and React did not handle it (gracefully) on next render. This could be due to the caching strategy of having to push from virtual to actual DOM so, the entire application crashes down. In React 16 however, a kind of try-catch for components is introduced as Error Boundaries to take care of this problem allowing you catch these errors before they get to the internals of the React application.

Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, and does something worthwhile with it like displaying a fallback interface instead of the component tree that crashed or logging the exact error. Error boundaries catch errors during rendering, in lifecycle methods, and in constructors of the whole tree below them, unmount the component tree while maintaining the usual workings and renderings of the rest of the React application.


**IMPORTANT!**

An Error Boundary in React is therefore defined as a Class Component that defines one or both of static ```getDerivedStateFromError()``` or ```componentDidCatch()``` lifecycle methods. The first one, static ```getDerivedStateFromError()``` is used to render a fallback user interface after an error has been thrown and the second one, ```componentDidCatch()``` is used to log error information to an error tracking service say Sentry. This is the official syntax below:

```js
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
     this.state = { hasError: false };
  }
  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }
  componentDidCatch(error, info) {
    // You can also log the error to an error reporting service
    logErrorToMyService(error, info);
  }
  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children; 
  }
}
```

Then you can use it as a regular component like thus:

```js
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

# API's

Application Programming Interface is a messanger that takes a request and tells the system what to do. 
Is the way that machines communicate to share information.

Ejemplo: 

**Turismo City use an API to make a request to each website belonging to Airlines to fetch the information that matches the flight you asked for** 

Example from Robofriends:

```js
componentDidMount() {
        fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(users => this.setState({ robots: users }))
    }
```
We use ```fetch()``` to bring information from _jsonplaceholder_ API.


# HTTP/HTTPS 

[HTTP/HTTPS by Andrei](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8766756#overview)

# JSON

[JSON by Andrei](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8766758#overview)

When exchanging data between a browser and a server, the data can only be text. So we can't just send a JavaScript object, because HTTP won't understund it but also because if we were sending this data to Googles Servers i.e, the server might not be built upon that same language. Text on the other hand, can be understund by all. That is what JSON is for. XML is not as efficient. 

* **JSON - JavaScript Object Notation**: it looks pretty much like an JS object. JSON uses JavaScript syntax, but the JSON format is text only. The JSON format is almost identical to JavaScript objects. In JSON, keys **must be strings**, written with double quotes. In JavaScript, keys can be strings, numbers, or identifier names.

* **JSON is a syntax for storing and exchanging data**: is it the only way? No, there is also, XML (eXtensible Markup Language). Both can be used to receive data from a web server. The standard is JSON.  

* **JSON is text, written with JavaScript object notation**:  everything has to be a string, even properties, whereas in JS, the property (key) doesn't have to be a string (wrapped around double quotes). When exchanging data between a browser and a server, the data can only be text. JSON is text, and we can convert any JavaScript object into JSON, and send JSON to the server. We can also convert any JSON received from the server into JavaScript objects. This way we can work with the data as JavaScript objects, with no complicated parsing and translations.

```JSON
{"employees":[  
    {"name":"Shyam", "email":"shyamjaiswal@gmail.com"},  
    {"name":"Bob", "email":"bob32@gmail.com"},  
    {"name":"Jai", "email":"jai87@gmail.com"}  
]}  
```

### Sending Data

If you have data stored in a JavaScript object, you can convert the object into JSON, and send it to a server:

Example

```js
var myObj = {name: "John", age: 31, city: "New York"};
var myJSON = JSON.stringify(myObj);
```

### Receiving Data

If you receive data in JSON format, you can convert it into a JavaScript object:

Example

```js
var myJSON = '{"name":"John", "age":31, "city":"New York"}';      
var myObj = JSON.parse(myJSON);
```

# AJAX

AJAX allows web pages to be updated asynchronously by exchanging data with a web server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

AJAX is a developer's dream, because you can:

* Read data from a web server - after the page has loaded
* Update a web page without reloading the page
* Send data to a web server - in the background

AJAX is not a programming language. **AJAX is a technique for accessing web servers from a web page.** AJAX stands for _Asynchronous JavaScript And XML_.

![How AJAX works - Diagram](https://www.w3schools.com/js/pic_ajax.gif)

## ```XMLHttpRequest```

The keystone of AJAX is the ```XMLHttpRequest``` object.

The ```XMLHttpRequest``` Object
All modern browsers support the ```XMLHttpRequest``` object.

The ```XMLHttpRequest``` object can be used to exchange data with a web server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

How to implement it:

```js
fetch('/my/url').then(response => {
    console.log(response);
});
```

## ```fetch()``` and ```Promise```

In JavaScript, a promise is an object that returns a value which you hope to receive in the future, but not now. Because the value will be returned by the promise in the future, the promise is very well-suited for handling asynchronous operations. 

A promise starts in the pending state which indicates that the promise hasn’t completed. It ends with either fulfilled (successful) or rejected (failed) state.

JavaScript can send network requests to the server and load new information whenever it’s needed. And all of that without reloading the page! That can be done with ```fetch()```

The basic syntax is:

```js
let promise = fetch(url, [options])
```

* ```url``` – the URL to access.
* ```options``` – optional parameters: method, headers etc.

**Without ```options```, that is a simple GET request, downloading the contents of the ```url```. The browser starts the request right away and returns a promise that the calling code should use to get the result.**

Getting a response is usually a two-stage process.

1. First, the ```promise```, returned by ```fetch```, resolves with an object of the built-in ```Response``` class as soon as the server responds with headers.

At this stage we can check HTTP status, to see whether it is successful or not, check headers, but don’t have the body yet.

The promise rejects if the ```fetch``` was unable to make HTTP-request, e.g. network problems, or there’s no such site.

We can see HTTP-status in response properties:

* ```status``` – HTTP status code, e.g. 200.
* ```ok``` – boolean, ```true``` if the HTTP status code is 200-299.

```js
let response = await fetch(url);

if (response.ok) { // if HTTP-status is 200-299
  // get the response body (the method explained below)
  let json = await response.json();
} else {
  alert("HTTP-Error: " + response.status);
}
```

2. Second, to get the response body, we need to use an additional method call.

Response provides multiple promise-based methods to access the body in various formats:

```response.text()``` – read the response and return as text,
```response.json()``` – parse the response as JSON,
```response.formData()``` – return the response as FormData object (explained in the next chapter),
```response.blob()``` – return the response as Blob (binary data with type),
```response.arrayBuffer()``` – return the response as ArrayBuffer (low-level representaion of binary data),
additionally, ```response.body``` is a ReadableStream object, it allows you to read the body chunk-by-chunk, we’ll see an example later.

For instance, let’s get a JSON-object with latest commits from GitHub:

```js
let url = 'https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits';
let response = await fetch(url);

let commits = await response.json(); // read response body and parse as JSON

alert(commits[0].author.login);
```

Or, the same without await, using pure promises syntax:

```js
fetch('https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits')
  .then(response => response.json())
  .then(commits => alert(commits[0].author.login));
```

### ```.json()``` method

**IMPORTANT**

The ```json()``` method of the ```Body``` mixin takes a ```Response``` stream and reads it to completion. It returns a promise that resolves with the result of parsing the body text as ```JSON```. To extract the JSON body content from the response, we use the ```json()``` method (defined on the Body mixin, which is implemented by both the Request and Response objects.)

Syntax

```js
response.json().then(data => {
  // do something with your data
});
```

### ```.then()``` method

[```.then()``` explained nicely](https://masteringjs.io/tutorials/fundamentals/then)

There's no way to get a promise's value from the promise directly - you need to call the ```then()``` function to register a callback that JavaScript will call when the value is computed.

The ```then()``` method returns a Promise. It takes up to two arguments: callback functions for the success and failure cases of the Promise.

```js
const promise1 = new Promise((resolve, reject) => {
  resolve('Success!');
});

promise1.then((value) => {
  console.log(value);
  // expected output: "Success!"
});
```

The ```then()``` Function's Parameters
The ```then()``` function takes 2 callback function parameters:

* ```onFulfilled()```: JavaScript will call this function if the underlying async operation succeeded.
* ```onRejected()```: JavaScript will call this function if the underlying async operation failed.

Both ```onFulfilled()``` and ```onRejected()``` are optional. If ```onFulfilled()``` is ```null```, JavaScript will do nothing if the promise is fulfilled. If you call ```.then()``` without an ```onRejected()``` function and the promise rejects, that will lead to an unhandled rejection error message.

Recall that a promise is a state machine with 3 states:

1. **Pending** The operation is in progress.
2. **Fulfilled** The operation completed successfully.
3. **Rejected** The operation experienced an error.

### ```fetch()```

[```fetch```, ```then()``` and ```.json()``` explained](https://www.sitepoint.com/introduction-to-the-fetch-api/#:~:text=The%20Fetch%20API%20provides%20a,the%20response%20of%20the%20request.)

**IMPORTANT!**

>The Fetch API provides a ```fetch()``` method defined on the ```window``` object, which you can use to perform requests. This method returns a ```Promise```, an object which represents a future result, that you can use to retrieve the response of the request. There's no way to get a promise's value from the promise directly - you need to call the ```then()``` function to register a callback that JavaScript will call when the value is computed. The ```json()``` method of the ```Body``` mixin takes a ```Response``` stream and reads it to completion. It returns a promise that resolves with the result of parsing the body text as ```JSON```. To extract the JSON body content from the response, we use the ```json()``` method

That said, the following code snippet is easy to understand.

```js
    componentDidMount() {
        fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(users => this.setState({ robots: users }))
    }
```

1. We start the request by calling ```fetch()```. 
2. When the promise is fulfilled, it returns a ```Response``` object, which exposes a ```json``` method. 
3. Within the first ```then()``` we can call this ```json``` method to return the response body as JSON.
4. However, the ```json``` method also returns a promise, which means we need to chain on another ```then()```, before the JSON response is logged to the console (in the snippet above, we don't log, we changed the state of ```robots```)

And why does ```json()``` return a promise? Because HTTP allows you to stream content (*transmitir contenido*) to the client chunk by chunk, so even if the browser receives a response from the server, the content body might not all be there yet!

### Promise

In JavaScript, a promise is an object that returns a value which you hope to receive in the future, but not now. A promise starts in the pending state which indicates that the promise hasn’t completed. It ends with either fulfilled (successful) or rejected (failed) state.

Because the value will be returned by the promise in the future, the promise is very well-suited for handling asynchronous operations.

A promise is a state machine with 3 states:

1. **Pending** The operation is in progress.
2. **Fulfilled** The operation completed successfully.
3. **Rejected** The operation experienced an error.

Before promises, what existed were callback functions. 

To create a promise in JavaScript, you use the ```Promise``` constructor:

```js
let completed = true;

let learnJS = new Promise(function (resolve, reject) {
    if (completed) {
        resolve("I have completed learning JS.");
    } else {
        reject("I haven't completed learning JS yet.");
    }
});

learnJS.then(result => console.log(result))
```

The ```Promise``` constructor accepts a function as an argument. This function is called the ```executor```.

The ```executor``` accepts two functions with the names, by convention, ```resolve()``` and ```reject().``` 

When you call the ```new Promise(executor)```, the ```executor``` is called automatically. 

Inside the ```executor```, you manually call the ```resolve()``` function if the ```executor``` is completed successfully and invoke the ```reject()``` function in case of an error occurs.

Once a new ```Promise``` object is created, it is in the pending state until it is resolved. To schedule a callback when the promise is either resolved or rejected, you call the methods of the ```Promise``` object: ```then()```, ```catch()```, and ```finally()```.

#### ```then()```

The ```then()``` method is used to schedule a callback to be executed when the promise is successfully resolved.

The ```then()``` method takes two callback functions:

```js
promiseObject.then(onFulfilled, onRejected);
```

The ```onFulfilled``` callback is called if the promise is fulfilled. The ```onRejected``` callback is called when the promise is rejected.

#### ```catch()```

If you want to schedule a callback to be executed when the promise is rejected, you can use the ```catch()``` method of the ```Promise``` object:

```js
learnJS.catch(
    reason => console.log(reason)
);
```

Internally, the ```catch()``` method invokes the ```then(undefined, onRejected)``` method.

**```catch()``` catches any error that may happen between the ```then()``` chain:**

```js
const promise = new Promise((resolve, reject) => {
    if (true) {
        resolve('Stuff worked');
    } else {
        reject('It didnt work');
    }
})

promise
.then(result => {
    throw Error
    return result + '!'
})
.then(result2 => console.log(result2))
.catch(() => console.log('errorrrr!'))
```

If an error happens after the ```catch``` statement, the ```catch``` won't be able to handle that error. 

**When you don't want JS to block the execution of your code, like making API calls, grabbing data from a database or optimizing an image, you would use a ```Promise``` so the task happens on the background.**

#### ```.finally()```

The ```finally()``` method returns a ```Promise```. When the promise is settled, i.e either fulfilled or rejected, the specified callback function is executed. This provides a way for code to be run whether the promise was fulfilled successfully or rejected once the ```Promise``` has been dealt with.

This helps to avoid duplicating code in both the promise's ```then()``` and ```catch()``` handlers.

The ```finally()``` method can be useful if you want to do some processing or cleanup once the promise is settled, regardless of its outcome.

```js
const urls = [
    "https://jsonplaceholder.typicode.com/users",
    "https://jsonplaceholder.typicode.com/posts",
    "https://jsonplaceholder.typicode.com/albums"
]

Promise.all(urls.map(url => {
    return fetch(url).then(resp => resp.json())
})).then(results => {
    console.log(results[0])
    console.log(results[1])
    console.log(results[2])
})
.catch(() => console.log('error'))
.finally(() => console.log('extra'));
```

#### ```setTimeOut()```

The ```setTimeout()``` method calls a function or evaluates an expression after a specified number of milliseconds.

Syntax

```js
setTimeout(function, milliseconds, param1, param2, ...)
```

_Example:_ 

```HTML
<!DOCTYPE html>
<html>
<body>

<p>Click on the button below. The input field will tell you when two, four, and six seconds have passed.</p>

<button onclick="timedText()">Display timed text</button>
<input type="text" id="txt">

<script>
function timedText() {
  var x = document.getElementById("txt");
  setTimeout(function(){ x.value="2 seconds" }, 2000);
  setTimeout(function(){ x.value="4 seconds" }, 4000);
  setTimeout(function(){ x.value="6 seconds" }, 6000);
}
</script>

</body>
</html>
```

#### ```setTimeOut()``` + ```Promise``` + ```Promise.all()```

The ```Promise.all()``` method takes an iterable of promises as an input, and returns a single ```Promise``` that resolves to an array of the results of the input promises. This returned promise will resolve when all of the input's promises have resolved, or if the input iterable contains no promises. It rejects immediately upon any of the input promises rejecting or non-promises throwing an error, and will reject with this first rejection message / error.

Syntax

```js
Promise.all(iterable);
```

```js

const promise = new Promise((resolve, reject) => {
    if (true) {
        resolve('The thing worked!');
    } else {
        reject('didnt work');
    }
})

const promise2 = new Promise((resolve, reject) => {
    setTimeout(resolve, 100, 'Hiii');
})

const promise3 = new Promise((resolve, reject) => {
    setTimeout(resolve, 1000, 'Pookiee');
})

const promise4 = new Promise((resolve, reject) => {
    setTimeout(resolve, 3000, 'Is it you?');
})

Promise.all([promise, promise2, promise3, promise4])
.then(values => {
    console.log(values);
})

// Promise {<pending>}
//     __proto__: Promise
//     [[PromiseStatus]]: "fulfilled"
//     [[PromiseValue]]: undefined

// (4) ["The thing worked!", "Hiii", "Pookiee", "Is it you?"]

```

### Promise - Real application

```js
const urls = [
    "https://jsonplaceholder.typicode.com/users",
    "https://jsonplaceholder.typicode.com/posts",
    "https://jsonplaceholder.typicode.com/albums"
]

Promise.all(urls.map(url => {
    return fetch(url).then(resp => resp.json())
})).then(results => {
    console.log(results[0])
    console.log(results[1])
    console.log(results[2])
})
// we can chain a catch in case there is an error
.catch(() => console.log('error'))

```


## ```async...await```

Async await is part of ES8 and is built on top of promises. The ```async...await``` syntax offers a new way to write more readable and scalable code to handle promises.    

An asynchronous JavaScript function can be created with the ```async``` keyword before the ```function``` name, or before ```()``` when using the async arrow function. An ```async``` function always returns a promise.

### ```async```

```js
function helloWorld() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('Hello World!');
    }, 2000);
  });
}

const msg = async function() { //Async Function Expression
  const msg = await helloWorld();
  console.log('Message:', msg);
}

const msg1 = async () => { //Async Arrow Function
  const msg = await helloWorld();
  console.log('Message:', msg);
}

msg(); // Message: Hello World! <-- after 2 seconds
msg1(); // Message: Hello World! <-- after 2 seconds
```

### ```await```

A JavaScript ```async``` function can contain statements preceded by an ```await``` operator. The operand of ```await``` is a promise. At an ```await``` expression, the execution of the ```async``` function is paused and waits for the operand promise to resolve. The ```await``` operator returns the promise’s resolved value. An ```await``` operand can only be used inside an ```async``` function.

The ```await``` expression causes ```async``` function execution to pause until a ```Promise``` is settled (that is, fulfilled or rejected), and to resume execution of the ```async``` function after fulfillment. When resumed, the value of the ```await``` expression is that of the fulfilled ```Promise```.

If the ```Promise``` is rejected, the ```await``` expression throws the rejected value.

**The JavaScript ```async...await``` syntax allows multiple promises to be initiated and then resolved for values when required during execution of the program. As an alternate to chaining ```.then()``` functions, it offers better maintainablity of the code and a close resemblance synchronous code.**

**Putting all together - Examle:**

_Conventional way:_ 

```js
fetch('http://jsonplaceholder.typicode.com/users')
.then(response => response.json())
.then(response2 => console.log(response2))
```

_```async...await``` way:_

```js
async function fetchUsers() {
    const resp = await fetch('http://jsonplaceholder.typicode.com/users');
    const data = await resp.json();
    console.log(data);
}
```

#### ```async...await``` with ```Promise.all()```

_Example:_

```js
const urls = [
    "https://jsonplaceholder.typicode.com/users",
    "https://jsonplaceholder.typicode.com/posts",
    "https://jsonplaceholder.typicode.com/albums"
]

const getData = async function() {
    const [ users, posts, albums ] = await Promise.all(urls.map(url =>
        fetch(url).then(resp => resp.json())
    ))
    console.log('users', users);
    console.log('posts', posts);
    console.log('albums', albums);
}
```

#### Async Function Error Handling

JavaScript ```async``` functions uses ```try...catch``` statements for error handling. This method allows shared error handling for synchronous and asynchronous code.

```js
const urls = [
    "https://jsonplaceholder.typicode.com/users",
    "https://jsonplaceholder.typicode.com/posts",
    "https://jsonplaceholder.typicode.com/albums"
]

const getData = async function() {
    try {
        const [ users, posts, albums ] = await Promise.all(urls.map(url =>
            fetch(url).then(resp => resp.json())
        ))
        console.log('users', users);
        console.log('posts', posts);
        console.log('albums', albums);
    } catch (e) {
        console.log(e)
    }
}
```


# Node.js

Allows us to build servers using JavaScript language. 

You can run ```node``` in the terminal by typing ```node```. Then, you can run a script like this:

```
node scriptName
```

Node has an object called ```global``` and also another important one called ```process```. Same happens with ```Module```

```js
console.log(__dirname);
// C:\Users\Marcos\Desktop\node
```

### Import a module

The following is the way to do it "manually" or oldschool

```js
const script2 = require('./script2.js');

const a = script2.largeNumber;
```

### Export a module

```js
const largeNumber = 356;

module.exports = {
    largeNumber: largeNumber
};
```

### 3 kind of modules in node.js

1. **Self-built Modules**

This is how you import a self-built module

```js
const script2 = require('./script2.js');
```

This is how you export a self-built module

```js
const largeNumber = 356;

module.exports = {
    largeNumber: largeNumber
};
```

2. **Built-in Modules**

Those that come pre-installed with node.

This is how you import a built-in module

```js
const fsModule = require('fs');
```
**```fs``` (_fs_ for _fyle system_) module allows you to read the file system and do many things such as read a file and extract how many times a words repeats in that text, similar what you can do with Python. ```fs``` is one of the core modules of Node JS which provides functions for interacting with the physical filesystem. It is useful to perform all file I/O operations synchronously and asynchronously.** 

[Popular methods with ```fs``` module](https://www.tutorialsteacher.com/nodejs/nodejs-file-system)

[Popular methods with ```http``` module](https://nodejs.dev/learn/the-nodejs-http-module)

The HTTP core module is a key module to Node.js networking.

It can be included using

```js
const http = require('http');
```

3. **npm packages**

Installing nodemon

```npm init -y``` (creates package.json and say yes to any prompt question) and then ```npm install nodemon --save-dev``` which install Nodemon package as a dev dependency, which we only use in development environment. When we release the app, it won't be included, because is only for development stage. 

To run the comand with CLI, in package.json replace the ```"test": "echo \"Error: no test specified\" && exit 1"``` script for ```"start": "nodemon"```. Node is gonna look in the ```.bin``` folder and run nodemon whenever you type ```npm start```. 

**This allows you not to stop and start the server everytime you want to run a new scripts; it remains opened and listening for changes in the scripts**

## Creating a server with Node.js

In order for _nodemon_ to listen to _server.js_ changes (the file where we are gonna build the server), we have to change ```"start": "nodemon"``` to ```"start": "nodemon server.js"```

```js
const http = require('http');

const server = http.createServer(() => {
    console.log('I hear you!');
})

//The parameter expects the port number to listen to. 
server.listen(3000);
```

If afterwards you run ```node server.js``` and go to ```http://localhost:3000/```, you will see in your terminal a message saying ```I hear you!```. And every time you refresh, it will display again and again. 

```http.createServer``` accepts two parameters:

1. ```request```
2. ```response```

Example for ```response```

```js
const http = require('http');

const server = http.createServer((request, response) => {
    response.setHeader('Content-Type', 'text/html');
    response.end('<h1>Helloooo</h1>');
})

//The parameter expects the port number to listen to. 
server.listen(3000);
```

Example for ```request```:

```js
const server = http.createServer((request, response) => {
    console.log(request.headers);
    console.log(request.methods);
    console.log(request.url);
    response.setHeader('Content-Type', 'text/html');
    response.end('<h1>Helloooo</h1>');
})

//The parameter expects the port number to listen to. 
server.listen(3000);
```

### Sending a JSON with Node.js

```js
const http = require('http');

const server = http.createServer((request, response) => {
    const user = {
        name: 'john',
        hobby: 'skating'
    }
    response.setHeader('Content-Type', 'application/json');
    response.end(JSON.stringify(user)); // convert user JS object into JSON object to be able
                                        // to communicate with the server back and forth
})

//The parameter expects the port number to listen to. 
server.listen(3000);
```

## Express.js

It's an alternative tool to build a server rather than building it from scratch with ```http``` module.

This is how you instantiate and start a server with ```express.js```

```js
const express = require('express');

const app = express();

app.listen(3000);
```

And this is how you send a ```response``` with ```express.js```

```js
const express = require('express');

const app = express();

app.get('/', (req, resp) => {
    resp.send('helloooo');  // you don't have to tell what kind of content-type you send
})

app.listen(3000);
```

Sending a JSON as response:

```js
app.get('/', (req, resp) => {
    const user = {
        user: 'Sally',
        age: 23,
        hobby: 'running'
    }
    resp.send(user); // Again, you don't have to tell what kind of content-type you send.
                    // Express figures it out by it self. 
})
```

### Express.js Middleware

[Express.js Middleware](https://developer.okta.com/blog/2018/09/13/build-and-understand-express-middleware-through-examples#:~:text=Express%20middleware%20are%20functions%20that,compromised%20wholly%20of%20middleware%20functions.)

**Express middleware are functions that execute during the lifecycle of a ```request``` to the Express server.** Each middleware has access to the HTTP ```request``` and ```response``` for each route (or path) it’s attached to. In fact, Express itself is compromised wholly of middleware functions. Additionally, middleware can either terminate the HTTP ```request``` or pass it on to another middleware function using ```next``` (more on that soon). This “chaining” of middleware allows you to compartmentalize your code and create reusable middleware.

The ```app.get()``` function is Application-level Middleware. You’ll notice the parameters passed to the method are ```req```, ```res```, and ```next```. These are the incoming request, the response being written, and a method to call to pass the call to the next middleware function once the current middleware is finished. In this case, once the response is sent, the function exits. You could also chain other middleware here by calling the ```next()``` method.

Using ```app.use()``` means that this middleware will be called for every call to the application. 

[How does ```app.use()``` work?](https://discuss.codecademy.com/t/how-does-app-use-work/384243)

### Postman

Postman is a software development tool. It enables people to test calls to APIs. Postman users enter data. The data is sent to a special web server address. Typically, information is returned, which Postman presents to the user. Is a popular API client that makes it easy for developers to create, share, test and document APIs. This is done by allowing users to create and save simple and complex HTTP/s requests, as well as read their responses.


#### Parsing forms with Express

To handle HTTP POST request in Express.js version 4 and above, you need to use a body-parser middleware module.

```body-parser``` extract the entire body portion of an incoming request stream and exposes it on ```req.body```. You don't need it per se, because you could do all of that yourself. However, it will most likely do what you want and save you the trouble. In 2019-april-2: in express@4.16.0 the body-parser middleware bundled with express

_So basically, body-parser parses your incoming request, assembles the chunks of bits containing your form data, then creates this body object for you and filled it with your form data._

Requesting info of Body HTML using express body-parser:

```js
// In Postman choose POST method, x-www-form-urlencoded, and add key and values. Also add the URL, and then 
// Whatever is below this comment add it inside the script

const express = require('express');

const app = express();

app.use(express.urlencoded({extended: false}));

app.post('/posting', (req, res) => {
    console.log(req.body); // This will show up in the console, following whatever 
                        // we put in the body in Postman app
})

// Terminal
// [Object: null prototype] { Name: 'Mauro', Apellido: 'Consolani' }
```

#### Parsing JSON with express

```js
// In Postman choose POST method, raw, JSON, and add info in JSON format. Also add the URL, and then 
// Whatever is below this comment add it inside the script

const express = require('express');

const app = express();

app.use(express.json());

app.post('/posting', (req, res) => {
    console.log(req.body); // This will show up in the console, following whatever 
                        // we put in the body in Postman app
})

// Terminal
// { user: 'jenny', hobby: 'tennis' }
```

### RESTful API

[RESTful API's - Andrei Neagoie](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8817400#overview)

Is a way to define our server so that it specifies what it can provide and how can we use it. 

**REST API's are _stateless_ meaning that calls can be made independantly one another and each calls contains all the data necessary to complete it self successfully.** The server doesn't have to memorize things. Each request that comes in has enough information that the server can responds with, regardless of who that person/client is. 

#### Request properties

* ```req``` most used properties:

```js
req.query
req.body
req.headers
req.params
```

1. ```req.query``` example:

Allows you to access the query string. 

```js
app.get('/', (req, res) => {
    //passed URL: http://localhost:3000/?name=mauro&age=26
    console.log(req.query);
})

// Terminal
// { name: 'mauro', age: '26' }
```

2. ```req.headers``` example:

```js
app.get('/', (req, res) => {
    console.log(req.headers);
    res.send('root endpoint');
})

// Terminal
// {
//   name: 'Sally',
//   'content-type': 'application/json',
//   'user-agent': 'PostmanRuntime/7.26.5',
//   accept: '*/*',
//   'postman-token': 'a862a0ed-405f-44dc-89e6-0bd394555c65',
//   host: 'localhost:3000',
//   'accept-encoding': 'gzip, deflate, br',
//   connection: 'keep-alive',
//   'content-length': '49'
// }
```

3. ```req.params``` example:

Use ```/:``` in the route to be able to grab the params entered in the query string.

```js
//In POSTMAN pass this URL localhost:3000/1234

app.get('/:id', (req, res) => {
    console.log(req.params);
    res.send('root endpoint');
})
// Terminal
// { id: '1234' }
```

#### Response properties

* Whenever we send a ```response``` object, we also want to send the status code of the response.

```js
app.get('/', (req, res) => {
    res.status(404).send('not found');
})
```

* Send a JSON response

The ```res.json()``` function takes a single parameter, an object obj, serializes it to JSON, and sends it in the HTTP response body.

Sending a response can be achieved by calling the ```res.send()``` method. The signature of this method looks like this: ```res.send([body])``` where the body can be any of the following: ```Buffer```, ```String```, an ```Object``` and an ```Array```.

Many developers out there are using Express to create RESTful APIs, and most of the time such APIs return JSON data. Now the question is of course, **should we use ```res.send()``` to return JSON data - since this method accepts objects as part of its argument - or should we use ```res.json()```**

```res.json()``` actually has some functionality that is related to JSON objects that we can't access when using ```res.send()```

To sum things up, ```res.json()``` allows for extra formatting of the JSON data - if this is not required ```res.send()``` can also be used to return a response object using Express



##### Responding with static assets

**What if we just want to send static assets? such as index.html, css files, javascript files**

```js
app.use(express.static('./public'))
// or
app.use(express.static(__dirname + '/public'))
// public is the folder with our static assets.
```

## Reading files with Node.js

### Reading files Async

```js
const fs = require('fs');

fs.readFile('./hello.txt', (err, data) => {
    if (err) {
        console.log(err);
    }
    console.log(data.toString('utf8')); 
})
```

Without ```toString()``` node returns a ```<Buffer>``` memory object. ```toString()``` allows you to encode the file content, in this case into UTF-8 protcol.


### Reading files Sync

```js
const file = fs.readFileSync('./hello.txt');
console.log(file.toString());
```

### Appending to a file

Asynchronously append data to a file, creating the file if it does not yet exist. ```data``` can be a string or a Buffer.

```js
fs.appendFile('message.txt', 'data to append', (err) => {
  if (err) throw err;
  console.log('The "data to append" was appended to file!');
});
```

### Writing to a file

```js
fileWritten = fs.writeFile('message.txt', 'write this', (err) => {
  if (err) throw err;
  console.log(fileWritten.toString());
});
```

### Deleting a file

Asynchronously removes a file or symbolic link. No arguments other than a possible exception are given to the completion callback.

```js
// Assuming that 'path/file.txt' is a regular file.
fs.unlink('path/file.txt', (err) => {
  if (err) throw err;
  console.log('path/file.txt was deleted');
});
```
```fs.unlink()``` will not work on a directory, empty or otherwise. To remove a directory, use ```fs.rmdir()```.

## ```bcrypt-node.js```

The bcrypt library on NPM makes it really easy to hash and compare passwords in Node. Bcrypt is the de facto way to hash and store passwords. 


[bcrypt-node.js](https://www.npmjs.com/package/bcrypt-nodejs)

## ```cors```

CORS is a node.js package for providing a Connect/Express middleware that can be used to enable CORS with various options. Enabling cors, in our case, allows us to fetch from ```app.js``` running in localhost port 3000 grab data from ```server.js``` which is running in localhost port 3001. 

[cors](https://www.npmjs.com/package/cors)

# Database

**NoSQL vs SQL**
>In SQL databases, you have to pre define a schema of relations between each table, with their primary and foreign key as it corresponds.

A SQL database structure would be something like this:

* Users table
* Tweets table
* Followers table

>In NoSQL databases, you don't need to define a schema. You can define it as you go. They are more flexible, looking more like folders, just assambling related information of any kind. 

MongoDB is **document oriented**. 

A NoSQL database structure would be something like this:

* User1
* User2
* User3

1. [Installing and Setting Up PostgreSQL for each OS](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8853506#questions/12456042)

2. [Intro to SQL: Querying and managing data](https://www.khanacademy.org/computing/computer-programming/sql)

3. [Codecademy: queries, aggregate functions and multiple tables](https://www.codecademy.com/learn/learn-sql)

4. [PostgreSQL vs MySQL vs SQLite](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems)

## PostgreSQL


1. **Launch postgres from command:** ```psql U- postgres```

2. **Enter password**

3. **Go to database directory**: ```\c databaseName```

### PostgreSQL commands:


* **Listing relationships**

```\d```

* **Exiting psql terminal**

```\q``` or ```ctrl + c```


* **Create a database:**  

```CREATE DATABASE test;``` -> ```test``` is the name for the database

* **Query data - basic command:** 

```SELECT * FROM table_name```

```sql
SELECT age, name, birthday FROM users;
```


* **Create a table:** 

```CREATE TABLE table_name (column_1 datatype, column_2 datatype, column_3 datatype);```

_Example:_

```sql
CREATE TABLE users (name text, age smallint, birthday date);
```

* **Insert data into a table**

```INSERT INTO table_name (column_1, column_2, column_3) VALUES (values_1, 'values_2', values_3);```

_Example:_

```sql
INSERT INTO users (name, age, birthday) VALUES ("Andrei", 31, "1930-01-25");
```


* **Create a new column in an existing table**

```ALTER TABLE table_name ADD column datatype;```

_Example:_

```sql
ALTER TABLE users ADD score smallint;
```


* **Update a columns value in an existing table**

```UPDATE table_name SET column = someValue WHERE column = condition;```

_Example:_

```sql
UPDATE users SET score = 50 WHERE name = "Andrei";

UPDATE users SET score = 100 WHERE name = "John" OR name = "Sally";
```


* **Conditional Selections**

```SELECT * FROM table_name WHERE column_name LIKE condition;```

```sql
SELECT * FROM users WHERE name LIKE 'A%';
```
This means: select all if name starts with an A. Percentage symbol means: anything after A, or whichever character. 

* **Select and order the selection**

```SELECT * FROM table_name ORDER BY column_name;```

```sql
SELECT * FROM users ORDER BY score DESC;
SELECT * FROM users ORDER BY score ASC;
```

* **Delete data from tables**

```DELETE FROM table_name WHERE column_name = condition;```

```sql
DELETE FROM users WHERE name = "Sally";
```

* **Delete Table**

```DROP TABLE table_name;```

```sql
DROP TABLE users;
```

**SQL FUNCTIONS**

* **Select and do the average**

```SELECT AVG(column_name) FROM table_name;```

```sql
SELECT AVG(scores) FROM users;
```

* **Select and do the sum**

```SELECT SUM(column_name) FROM table_name;```

```sql
SELECT SUM(age) FROM users;
```

* **Select and count**

```SELECT COUNT(column_name) FROM table_name;```

```sql
SELECT COUNT(id) FROM users;
```

#### Joining Tables 

Let's create a table first:

```sql
CREATE TABLE login (
    ID serial NOT NULL PRIMARY KEY,
    secret VARCHAR(100) NOT NULL,
    name text UNIQUE NOT NULL
);
```

Let's insert data into it:

```sql
INSERT INTO login(secret, name) VALUES ("abc", "Andrei");
```
No need to insert data for ID column because it is a serial, meaning that is an integer that increases itself automatically. 

_Additional Note:_
>When we create a ```PRIMARY KEY``` inside a table, it creates another file that contains that ```PRIMARY KEY```, and the if you try ```\d``` command you will find that the data type of that file is ```sequence```. Internally, Postgres is gonna use that sequence file to grab that from the table it corresponds to. 

**To join tables, you must have a shared value between tables. Generally, this is called ```FOREIGN KEY```**


**JOINING TABLES**

```SELECT * FROM table_name JOIN other_table_name ON table_name.primary_key = other_table_name.foreign_key;```

The ```ON``` keyword means: what are we gonna join them on; how is it gonna know what matches one table from the other. 

_Example:_

```sql
SELECT * FROM users JOIN login ON users.name = login.name;
```

## KNEX.js

We will use KNEX.js to associate the application with the server

[KNEX.js](http://knexjs.org/)

Install: 

```npm install knex```

Then install whatever database you are going to use. In our case, PostgreSQL

```npm install pg```

If you query something to your DB with a command like this:

```js
postgres.select('*').from('users')
```

You will then have to grab the information using ```then()```, given that what it gets returned is a promise. 
So we would do something like this:

```js
postgres.select('*').from('users').then(data => {
    console.log(data)
})
```
Remember, we don't do ```.then(response => response.json())``` because we are not connecting through HTTP, we are just quering the database. 

_Example:_

```js
db('users').insert({
    email: email,
    name: name,
    joined: new Date(),
}).then(console.log)
```

Full snippet: 

```js
app.post('/register', (req, res) => {
    const { name, email, password } = req.body;
    bcrypt.hash(password, null, null, function(err, hash) {
        console.log(hash);
    });

    db('users') 
    .returning('*')
    .insert({
        email: email,
        name: name,
        joined: new Date(),
    })
    .then(response => {
        res.json(response)
    })
})
```

The ```returning``` method specifies which column should be returned by the ```insert``` and ```update``` methods. Passed column parameter may be a string or an array of strings. When passed in a string, makes the SQL result be reported as an array of values from the specified column. When passed in an array of strings, makes the SQL result be reported as an array of objects.

_Additional Note:_
>_What are **transactions** in database managment?:_ A transaction is a unit of work that you want to treat as "a whole." It has to either happen in full or not at all. A transaction is a mechanism that allows you to mark a group of operations and execute them in such a way that either they all execute (commit), or the system state will be as if they have not started to execute at all (rollback). 

>**This is important because if you have to insert data on a table and a piece of that data in other table, but the 1st operation failed, well, then this last operation won't go through either, thanks to the transaction concept**

>Thus, transactions are an important feature of relational databases, as they allow correct recovery from failures and keep a database consistent even in cases of system failure. All queries within a transaction are executed on the same database connection, and run the entire set of queries as a single unit of work. Any failure will mean the database will rollback any queries executed on that connection to the pre-transaction state.

_Example:_

```js
db.transaction(trx => {
    trx.insert({
        hash: hash,
        email: email,
    })
    .into('login')
    .returning('email')
    .then(loginEmail => {
        return trx('users')
        .returning('*')
        .insert({
            email: loginEmail[0],
            name: name,
            joined: new Date(),
        }).then(user => {
            res.json(user[0]);
            })
        }).then(trx.commit)
        .catch(trx.rollback)
    }).catch(err => res.status(400).json('unable to register'))

```

____

_Addtional Note:_
>Dependency Injection is a pattern where, instead of creating or requiring dependencies directly inside a module, we pass them as parameters or reference.

[Dependency Injection](https://tsh.io/blog/dependency-injection-in-node-js/)

____


# Environmental Variables

Getting access to environmental variables of the OS.

```js
console.log(process.env)
```

_Example:_

```js
app.listen(process.env.PORT, () => {
    console.log(`Server listening at port ${process.env.PORT}`);
})
```

But to be able to access to that PORT, first, we have to inject it in the environment of the computer where the server is going to be running. 

To set an env variable in bash, such as PORT, you can do the following:

```
PORT=3001 node server.js
```

# Deploy

## Server Deployment - Heroku

[Deploying React app in Heroku](https://medium.com/quick-code/deploying-production-build-of-react-app-to-heroku-2548d8bf6936)

[Deploying server in Heroku - Andrei Neagoie](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8915976#questions)

* ```heroku login```
Logs you into the Heroky CLI

* ```heroku create```
Creates a Heroku APP

* ```heroku git:remote -a appName```
Tells Github which app from Heroku associate to

* ```heroku open```
Opens in the browser the application deployed in Heroku

* ```heroku log --tail```
Allows you too see the errors and logs happening in the heroku deployed app

* ```git remote -v```
Allows you to see to what Heroku app is this repository linked to

* ```git push heroku master```
Pushes you code from the GIT repository to your Heroku app


## Database Deployment - Heroku

[PostgreSQL Deployment in Heroku - Andrei Neagoie](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/8915539#questions)

* ```heroku addons```
This will display the addons you have in your current application.  

* ```heroku pg:info```
Shows data related to the postgreSQL database

* ```heroku pg:psql```
Allows you to connect to the database

* ```heroku config```
Gives us data like database URL

## Frontend Deployment - Heroku

[Deployment of React App - Create React App Doc](https://create-react-app.dev/docs/deployment/#static-server)

[Deployment of React App in Heroku - Create React App Doc ](https://create-react-app.dev/docs/deployment/#heroku)

# State Management

[Speaking about states - Andrei Neagoie](https://www.udemy.com/course/the-complete-web-developer-zero-to-mastery/learn/lecture/10175200#questions)

## Redux

[Redux made easy](https://dev.to/dylanmesty/redux-basics-explained-from-a-beginner-s-perspective-abm#:~:text=Redux%20has%20one%20main%20advantage,Redux%20is%20Uber%20Eats.)

Why do we wanna use redux?

1. Good for managing large state
2. Useful for sharing data between containers
3. Predictable state management using the 3 principles
    
    * Single source of truth:
    The idea of having one single big object that describes the entire state of the app.

    * State is read only:
    This relates to _inmutability_ concept: not modifying the main object to prevent unexpected errors. The state object that we create with redux will actually never get modified, and instead we will create a new state after each action is taken by the user. 

    * Changes using pure functions:
    The idea that a pure function is something that receives an input and always return an output that is predictable. 

### Redux Vocabulary

1. **Action:** is something a user does, such as clicking on abutton or a dropdown menu.

2. **Reducer:** as soon as a user performs and _action_, that _action_ goes through something called _reducer_. A _reducer_ is a function; a pure function that receives an input (the _action_) and creates an output, and this output is the state or the _store_. 

3. **Store:** this represents the entire state of the app. 

4. **Make Changes:** when an _action_ is performed, a _reducer_ function gets triggered, affecting the _store_, which triggers React to _make changes_ in the application. 

Redux uses an architectural pattern called **Flux Pattern**. This pattern triggered the idea of Redux, because in consists on having an action, deliver it to a dispatcher, that dispatches the action to the store which updates the view, following a one-way-data-flow. 

Before this pattern, the most used was **MVC** for _Module View Controller_. The idea with an MVC pattern is that we have an action, and that action is read by a controller (a JS file), and based on whatever the controller says, we update the model (data or state), and then updates the view. The problems of this pattern is that a change in a model can trigger a change in the view; and that change in the view can trigger a change in a model and so on, causing a chain of actions hard to trace and to debug in any case.  

### Installing Redux

1. ```npm install redux```


2. It is also necessary to install the library than binds React and Redux. React-Redux its only going to connect only the containers such as App.js to the Redux Store. This way, the container can communcicate to the store and viceversa. 

```npm install react-redux``` 

### Creating a reducer

Vocab: **Payload**

Payload is what is bundled in your actions and passed around between reducers in your redux application. For example:

```js
const someAction = {
  type: "Test",
  payload: {user: "Test User", age: 25},
}
```

This is a generally accepted convention to have a type and a payload for an action. The payload can be any valid JS type ( array , object, etc ).

Hope this clarifies your doubt!


____

_About **Payload** meaning

_Additional Note:_
>The term 'payload' is used to distinguish between the 'interesting' information in a chunk of data or similar, and the overhead to support it. It is borrowed from transportation, where it refers to the part of the load that 'pays': for example, a tanker truck may carry 20 tons of oil, but the fully loaded vehicle weighs much more than that - there's the vehicle itself, the driver, fuel, the tank, etc. It costs money to move all these, but the customer only cares about (and pays for) the oil, hence, 'pay-load'.

>In programming, the most common usage of the term is in the context of message protocols, to differentiate the protocol overhead from the actual data. Take, for example, a JSON web service response that might look like this (formatted for readability):

```JSON
{
    "status":"OK",
    "data":
        {
            "message":"Hello, world!"
        }
}
```
>In this example, the string Hello, world! is the payload, the part that the recipient is interested in; the rest, while vital information, is protocol overhead.
____


**IMPORTANT!**

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore} from 'redux'
import App from './containers/App';
import * as serviceWorker from './serviceWorker';
import { searchRobots } from './reducers';

const store = createStore(searchRobots)

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App/>
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);

```

For future clearness:

*We created the ```<Provider store={store}>``` component that passes down the ```store```, the ```store``` uses the ```rootReducers``` or in this case, ```searchRobots``` reducer to create the store and create the object tree ```store``` that represents our state. The ```connect``` method from react-redux library, allows other components to be aware and listening for changes in the ```store```. Those components that will be aware of changes, may as well be called _smart components_ but preferably _containers_.



```js
import { connect } from 'react-redux'; //this on top with all other imports

class App extends Component {
    //app and methods and stuff here
}


export default connect(mapStateToProps, mapDispatchToProps)(App); //this on bottom
```

This tells ```App``` component to subscribe to any state changes in the redux store. And now ```App``` knows that there is a redux store somewhere and any time there are changes in it, ```App``` might be interested in it. 

Afterwards, we have to tell the ```App``` component what actions to listen to. Thus, we must define ```mapStateToProps``` and ```mapDispatchToProps``` functions.

```js
const mapStateToProps = state => {
    return {
        searchField: state.searchRobots.searchField
    }
}

const mapDispatchToProps = (dispatch) => {
    return {
        onSearchChange: (event) => dispatch(setSearchField(event.target.value))
    } 
}
```

```mapStateToProps``` will tell us what piece of state I need to listen to and then pass it down as ```props``` and ```mapDispatchToProps``` asks for that prop that it must listen to because it will dispatch or trigger an action. 

```mapStateToProps``` is a function that you would use to provide the store data to your component, whereas ```mapDispatchToProps``` is something that you will use to provide the action creators as props to your component.

### redux-logger

One of the greatest strengths of Redux is debuggability — by logging actions and state during an app’s execution, developers can easily understand code errors, race conditions, network errors and other sources of bugs.

In local development it is standard practice to use tools like redux-logger or redux-devtools for time-travel debugging and viewing Redux actions. But the benefits of using Redux logs to easily fix bugs are most significant in production.

```js
import { createLogger } from 'redux-logger'

const logger = createLogger();
```

Also, we must import he ```applyMiddleware``` package from ```react-redux``` for redux logger to work.  

```js
import { createStore, applyMiddleware} from 'redux'
```

And then, pass all as a parameter to the ```createStore``` method:

```js
const store = createStore(searchRobots, applyMiddleware(logger))
```

Now, if you type something in the Robofriends app and go to the console, you will see something like this:

```js
action CHANGE_SEARCH_FIELD @ 12:56:52.888
    prev state {searchField: ""}
        action     
        {type: "CHANGE_SEARCH_FIELD", payload: "a"}
            payload: "a"type: "CHANGE_SEARCH_FIELD"
            __proto__: Object
        next state {searchField: "a"}
```

### Redux Async Actions

[Redux Async Actions & redux-thunk](https://www.digitalocean.com/community/tutorials/redux-redux-thunk#:~:text=Redux%20Thunk%20is%20a%20middleware,asynchronous%20operations%20have%20been%20completed.)

There are two very popular middleware libraries that allow for side effects and asynchronous actions: Redux Thunk and Redux Saga.

Thunk is a programming concept where a function is used to delay the evaluation/calculation of an operation.

Redux Thunk is a middleware that lets you call action creators that return a function instead of an action object. That function receives the store’s dispatch method, which is then used to dispatch regular synchronous actions inside the function’s body once the asynchronous operations have been completed.

```npm install redux-thunk```

Then import it to ```index.js```:

```js
import { thunkMiddleware } from 'redux-thunk';
```

And add it to the ```applyMiddleware``` redux function:

```js
const store = createStore(searchRobots, applyMiddleware(thunkMiddleware, logger))
```

Then, we have to build the constant variables in ```constant.js```. Given that we are going to try to replace with Redux a fetch function, which naturally returns a promise with three different states, we will have to declare three different constants. This is a standard with all asynchronous actions like AJAX calls. 

```js
export const REQUEST_ROBOTS_PENDING = 'REQUEST_ROBOTS_PENDING';
export const REQUEST_ROBOTS_SUCCESS = 'REQUEST_ROBOTS_SUCCESS';
export const REQUEST_ROBOTS_FAILED = 'REQUEST_ROBOTS_FAILED';
```

Afterwards, we need to create the actions in ```actions.js```

```js
import { 
    CHANGE_SEARCH_FIELD,
    REQUEST_ROBOTS_PENDING,
    REQUEST_ROBOTS_SUCCESS,
    REQUEST_ROBOTS_FAILED
 } from './constant.js';

export const requestRobots = (dispatch) => {
    dispatch({ type: REQUEST_ROBOTS_PENDING });
    fetch('https://jsonplaceholder.typicode.com/users')
    .then(data => dispatch({type: REQUEST_ROBOTS_SUCCESS, payload: data}))
    .catch(err => dispatch({type: REQUEST_ROBOTS_FAILED, payload: err}))
}
```

Then, we must create the reducer. 

```js
import {
    REQUEST_ROBOTS_PENDING,
    REQUEST_ROBOTS_SUCCESS,
    REQUEST_ROBOTS_FAILED
} from './constant.js';

const initialStateRobots = {
    isPending: false,
    robots:[],
    error: ''
}

export const requestRobots = (state=initialStateRobots, action={}) => {
    switch(action.type) {
        case REQUEST_ROBOTS_PENDING:
            return Object.assign({}, state, { isPending: true });
        case REQUEST_ROBOTS_SUCCESS:
            return Object.assign({}, state, { robots:action.payload, isPending: false });
        case REQUEST_ROBOTS_FAILED:
            return Object.assign({}, state, { error: action.payload, isPending: false });
        default: 
            return state;
    }
}
```

Once we have done that, we have to import the new reducer into our ```index.js``` to be able to pass it down to the application. If we have more than one reducer, we have to use a redux method that allows us to combine reducers.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import { createStore, applyMiddleware, combineReducers} from 'redux'; // <--------
import { createLogger} from 'redux-logger';
import thunkMiddleware from 'redux-thunk';
import './index.css';
import App from './containers/App';
import * as serviceWorker from './serviceWorker';
import 'tachyons';
import { searchRobots, requestRobots } from './reducers'; // <--------

const logger = createLogger();
const rootReducer = combineReducers({searchRobots, requestRobots}) // <--------
const store = createStore(rootReducer, applyMiddleware(thunkMiddleware, logger)) // <--------

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <App/>
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);
```

Up until this point, our ```mapStateToProps``` in ```App.js``` might be looking something like this:

```js
const mapStateToProps = state => {
    return {
        searchField: state.searchRobots.searchField
    }
}
```

Going back to redux-thunk, it is a middleware that weights and sees if any actions return a function instead of an object. Let see:

This action returns an object:

```js
export const setSearchField = (text) => ({
    type: CHANGE_SEARCH_FIELD,
    payload: text
})
```

This action doesnt return an object:

```js
export const requestRobots = (dispatch) => {
    dispatch({ type: REQUEST_ROBOTS_PENDING });
    fetch('https://jsonplaceholder.typicode.com/users')
    .then(data => dispatch({type: REQUEST_ROBOTS_SUCCESS, payload: data}))
    .catch(err => dispatch({type: REQUEST_ROBOTS_FAILED, payload: err}))
}
```

If react-thunk (thunkMiddleware) notices a function, its gonna act upon it. Let see some code to show how it works.

In ```App.js```

```js
const mapStateToProps = state => {
    return {
        searchField: state.searchRobots.searchField,
        robots: state.requestRobots.robots,
        isPending: state.requestRobots.isPending,
        error: state.requestRobots.error
    }
}

const mapDispatchToProps = (dispatch) => {
    return {
        onSearchChange: (event) => dispatch(setSearchField(event.target.value)),
        onRequestRobots: () => dispatch(requestRobots())
    } 
}
```

In ```actions.js``` create a high order function that receives ```dispatch``` as the argument of the second function triggered by ```onRequestRobots``` function property (see above)

```js
export const requestRobots = () => (dispatch) => {
    dispatch({ type: REQUEST_ROBOTS_PENDING });
    fetch('https://jsonplaceholder.typicode.com/users')
    .then(response => response.json())
    .then(data => dispatch({type: REQUEST_ROBOTS_SUCCESS, payload: data}))
    .catch(err => dispatch({type: REQUEST_ROBOTS_FAILED, payload: err}))
}
```

In ```App.js``` we have to change the lifecycle hook ```componentDidMount()```:

```js
componentDidMount() {
    this.props.onRequestRobots()
}
```

And also we don't need the ```constructor()``` method neither ```super()``` so we can erase them, and destructure ```this.state.robots``` to the other props rendered:

```js
render() {
        const { robots, searchField, onSearchChange, isPending } = this.props;
        const filteredRobots = robots.filter(robot => {
            return robot.name.toLowerCase().includes(searchField.toLowerCase());
        })
        return isPending ?
        <h1>Loading</h1>: 
        (
            <div className="tc">
                <h1 className="f2">Robofriends</h1>
                <SearchBox searchChange = {onSearchChange}/>
                <Scroll>
                    <ErrorBoundary>
                        <CardList robots={filteredRobots} />
                    </ErrorBoundary>
                </Scroll>
            </div>
        );
    
    }
```

# React useful tools 

1. **React Router**: allows to route your pages.
2. **Rambda**: utility library. 
3. **Lodash**: utility library. 
4. **Glamorous.rocks**: styling library 
5. **styled-components**: styling library 
6. **CSS Modules**: styling library 
7. **Gatsby.js**: styling library
8. **Next.js**: popular for server side rendered apps
9. **Material UI**: styling library
10. **Semantic UI**: styling library
11. **reselect**: selector library for Redux
11. **Redux-Saga**: helps to make application side effects easier to manage, like AJAX actions with redux. Similar to redux-thunk
12. **Immutable.js**: to help state to remain immutable and enforce that among developer team


# React Hooks

Hooks are functions that let you “hook into” React state and lifecycle features from function components. Hooks don’t work inside classes — they let you use React without classes.

## Why Hooks?

1. **It’s hard to reuse stateful logic between components:** with Hooks, you can extract stateful logic from a component so it can be tested independently and reused. _Hooks allow you to reuse stateful logic without changing your component hierarchy._ This makes it easy to share Hooks among many components or with the community.

2. **Complex components become hard to understand:** we’ve often had to maintain components that started out simple but grew into an unmanageable mess of stateful logic and side effects. In many cases it’s not possible to break these components into smaller ones because the stateful logic is all over the place. To solve this, _Hooks let you split one component into smaller functions based on what pieces are related (such as setting up a subscription or fetching data), rather than forcing a split based on lifecycle methods._

3. **Classes confuse both people and machines:** classes can be a large barrier to learning React. Classes don’t minify very well, and they make hot reloading flaky and unreliable. _Hooks let you use more of React’s features without classes. Conceptually, React components have always been closer to functions._

### State Hook

[State Hooks - React Doc](https://reactjs.org/docs/hooks-state.html)

This example renders a counter. When you click the button, it increments the value:

```js
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Here, ```useState``` is a Hook. We call it inside a function component to add some local state to it. React will preserve this state between re-renders. **```useState``` returns a pair: the current state value and a function that lets you update it. You can call this function from an event handler or somewhere else.** It’s similar to ```this.setState``` in a class, except it doesn’t merge the old and new state together.

____

**IMPORTANT!**
**Array Destructuring**

```js
const [fruit, setFruit] = useState('banana');
```

This JavaScript syntax is called “array destructuring”. It means that we’re making two new variables ```fruit``` and ```setFruit```, where ```fruit``` is set to the first value returned by ```useState```, and ```setFruit``` is the second. It is equivalent to this code:

```js
  var fruitStateVariable = useState('banana'); // Returns a pair
  var fruit = fruitStateVariable[0]; // First item in a pair
  var setFruit = fruitStateVariable[1]; // Second item in a pair
```

When we declare a state variable with ```useState```, it returns a pair — an array with two items. The first item is the current value, and the second is a function that lets us update it. Using ```[0]``` and ```[1]``` to access them is a bit confusing because they have a specific meaning. This is why we use array destructuring instead.

____

**The only argument to ```useState``` is the initial state.** In the example above, it is ```0``` because our counter starts from zero. Note that unlike ```this.state```, the state here doesn’t have to be an object — although it can be if you want.

#### Multiple State variables

You can use the State Hook more than once in a single component:

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

The array destructuring syntax lets us give different names to the state variables we declared by calling ```useState```. 

### Effect Hook

[Effect Hooks - React Docs](https://reactjs.org/docs/hooks-effect.html)

You’ve likely performed data fetching, subscriptions, or manually changing the DOM from React components before. We call these operations “side effects” (or “effects” for short) because they can affect other components and can’t be done during rendering.

The Effect Hook, ```useEffect```, adds the ability to perform side effects from a function component. It serves the same purpose as ```componentDidMount```, ```componentDidUpdate```, and ```componentWillUnmount``` in React classes, but unified into a single API.

For example, this component sets the document title after React updates the DOM:

```js
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

When you call ```useEffect```, you’re telling React to run your “effect” function after flushing changes to the DOM. Effects are declared inside the component so they have access to its props and state. By default, React runs the effects after every render — including the first render.

There are two common kinds of side effects in React components: 

1. Those that don’t require cleanup,
2. and those that do. 

Let’s look at this distinction in more detail.

#### Effects Without Cleanup

```js
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Sometimes, we want to run some additional code after React has updated the DOM. Network requests, manual DOM mutations, and logging are common examples of effects that don’t require a cleanup. We say that because we can run them and immediately forget about them.

We typically want to perform our effects after React has updated the DOM. This is why in React classes, we put side effects into ```componentDidMount``` and ```componentDidUpdate```

What does ```useEffect``` do? By using this Hook, you tell React that your component needs to do something after render. React will remember the function you passed, and call it later after performing the DOM updates.

Does ```useEffect``` run after every render? Yes! By default, it runs both after the first render and after every update. 

#### Effects with Cleanup

We looked at how to express side effects that don’t require any cleanup. However, some effects do.

You might be thinking that we’d need a separate effect to perform the cleanup. But code for adding and removing a subscription is so tightly related that ```useEffect``` is designed to keep it together. If your effect returns a function, React will run it when it is time to clean up:

```js
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

**Why did we return a function from our effect?** This is the optional cleanup mechanism for effects. Every effect may return a function that cleans up after it. This lets us keep the logic for adding and removing subscriptions close to each other. They’re part of the same effect!

**When exactly does React clean up an effect?** React performs the cleanup when the component unmounts. However, as we learned earlier, effects run for every render and not just once. This is why React also cleans up effects from the previous render before running the effects next time. We’ll discuss why this helps avoid bugs and how to opt out of this behavior in case it creates performance issues later below.

#### Avoiding infinite loops with Effect Hook

**Optimizing Performance by Skipping Effects**

In some cases, cleaning up or applying the effect after every render might create a performance problem. In class components, we can solve this by writing an extra comparison with ```prevProps``` or ```prevState``` inside ```componentDidUpdate```:

```js
componentDidUpdate(prevProps, prevState) {
  if (prevState.count !== this.state.count) {
    document.title = `You clicked ${this.state.count} times`;
  }
}
```

This requirement is common enough that it is built into the ```useEffect``` Hook API. **You can tell React to skip applying an effect if certain values haven’t changed between re-renders. To do so, pass an array as an optional second argument to ```useEffect```:**

```js
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

In the example above, we pass ```[count]``` as the second argument. What does this mean? If the ```count``` is ```5```, and then our component re-renders with ```count``` still equal to ```5```, React will compare ```[5]``` from the previous render and ```[5]``` from the next render. Because all items in the array are the same (```5 === 5```), React would skip the effect. That’s our optimization.

When we render with ```count``` updated to ```6```, React will compare the items in the ```[5]``` array from the previous render to items in the ```[6]``` array from the next render. This time, React will re-apply the effect because ```5 !== 6```. If there are multiple items in the array, React will re-run the effect even if just one of them is different.

### Rules of Hooks

Hooks are JavaScript functions, but they impose two additional rules:

1. Only call Hooks at the top level. Don’t call Hooks inside loops, conditions, or nested functions.

2. Only call Hooks from React function components. Don’t call Hooks from regular JavaScript functions. (There is just one other valid place to call Hooks — your own custom Hooks.)

____

**IMPORTANT!**

Video explaining the meaning of ```this``` and what it means in React components, and why are we able to use it in a class component.

[Meaning of this - Yihua Zheng](https://www.udemy.com/course/complete-react-developer-zero-to-mastery/learn/lecture/14870617#questions)

____

