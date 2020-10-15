
# Attributes

* _colspan_: cantidad de celdas que ocupa la columna. If ```colspan=2```, the column is gonna be 2 column wide
* _rowspan_: cantidad de celdas que ocupa la fila. If ```rowspan=2```, the row is gonna be 2 rows wide


# Day 3 

### Entity Codes

_From MDN:_
>An HTML entity is a piece of text ("string") that begins with an ampersand (&) and ends with a semicolon (;) . Entities are frequently used to display reserved characters (which would otherwise be interpreted as HTML code), and invisible characters (like non-breaking spaces). You can also use them in place of other characters that are difficult to type with a standard keyboard.

>For example, if you use the less-than (<) sign, the browser interprets any text that follows as a tag. 

To display these characters as text, replace them with their corresponding character entities, as shown in the following table.

**&** - **&amp;** - Interpreted as the beginning of an entity or character reference.

**<** - **&lt;** - Interpreted as the beginning of a tag

**>** - **&gt;** - Interpreted as the ending of a tag

**"** - **&quot;** - Interpreted as the beginning and end of an attribute's value.


[Full list of entity characters](https://dev.w3.org/html5/html-author/charref)


### Tables

```html
<table> - Wraps the whole table
<thead> - Wraps the header
<td> - Table Data; specifies the info that goes in each cell
<tr> - Table Row; Creates a row
<th> - Table Heading; specifies the info that goes in each header cell
<tbody> - Wrapes the body (excludes header and footer)
<tfoot> - Wraps the footer
<colgroup> - 
<caption> - Es el encargado de darle un título descriptivo a las tablas. It's the very first child of the table.
```

**DEPLOY THIS CODE TO UNDERSTUND THE THEORY**

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    table,tr,th,td {
        border:1px solid #000;
        border-collapse: collapse;
    }
</style>

<body>
    <h1>First Version</h1>
    <table>
        <thead>
            <caption>Table about trees</caption>
            <tr>
                <th>Species</th>
                <th>Diameter</th>
                <th>Tree Name</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Sequoia</td>
                <td>2</td>
                <td>Alerce</td>
            </tr>
            <tr>
                <td>Alamitus</td>
                <td>0.5</td>
                <td>Alamo</td>
            </tr>
            <tr>
                <td>Cipres</td>
                <td>1</td>
                <td>Pino</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>Average Diameter</td>
                <td>1</td>
                <td>None</td>
            </tr>
        </tfoot>
    </table>

    <h1>Second Version</h1>
    <table>
        <thead>
            <caption>Table about trees</caption>
            <tr>
                <th rowspan="2">Species</th>
                <th colspan="2">Diameter</th>
                <th rowspan="2">Tree Name</th>
            </tr>
            <tr>
                <th>Feet</th>
                <th>Meters</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Sequoia</td>
                <td>5</td>
                <td>2</td>
                <td>Alerce</td>
            </tr>
            <tr>
                <td>Alamitus</td>
                <td>3</td>
                <td>0.5</td>
                <td>Alamo</td>
            </tr>
            <tr>
                <td>Cipres</td>
                <td>3</td>
                <td>1</td>
                <td>Pino</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>Average Diameter</td>
                <td>3</td>
                <td>1</td>
            </tr>
        </tfoot>
    </table>
    
</body>
</html>
```

# Day 4


### **```<input>``` elemnt**:

The HTML ```<input>``` element is used to create interactive controls for web-based forms in order to accept data from the user; a wide variety of types of input data and control widgets are available, depending on the device and user agent. The ```<input>``` element is one of the most powerful and complex in all of HTML due to the sheer number of combinations of input types and attributes.

How an ```<input>``` works varies considerably depending on the value of its type attribute. If this attribute is not specified, the default type adopted is text.

Most commons types are:

1. text
2. password
3. number
4. email
5. color
6. file
7. submit
8. radio
9. checkbox

Besides the ```type``` and ```placeholder``` attribute, another important one is the ```name``` attribute.

* ````name``` attribute will be used to label the data when the form is sent/posted to a server somewhere. 

### **Why are ```<label>``` important:**

1. Each label is associated to a particular input
2. Accesibility purposes

You can associate the label to the input with 2 ways:

1. Wrapping the input with the label:

```html
<label for="">
    <input type="text" placeholder="write something">
</label>
```

2. Associating it with an ```id```attribute:

```html
<label for="textInput">
    <input type="text" id="textInput" placeholder="write something">
</label>
```

The second one is the most popular.


### The ```<form></form>``` element

The ```<form>``` element represents a document section containing interactive controls for submitting information. Is a container that holds a bunch of inputs, basically.

All the information in that form, once submitted, will be sent as a http request. 

* The ```action``` attribute let us specify where the form data should be submitted to. 

Example:

```html
<form action="https://www.reddit.com/search/">
    <input type="text" name="q" id="">
    <input type="submit" value="go">
</form>
```
  
This submits the data into the reddit url passed in as ```action``` attribute. ```q``` is the parameter Reddit expects for queries requests. Then, we write something and submit that form.


### Radio checkbox input

Remember to set the same ```name``` attribute for every radio input to associate them and avoid multiple selection.

```html
<input type="radio" id="Red" name="colors" value="red">
<label for="Red">Red</label>

<input type="radio" id="Orange" name="colors" value="orange">
<label for="Orange">Orange</label>

<input type="radio" id="Blue" name="colors" value="blue">
<label for="Blue">Blue</label>
```

**To submit an actual value when picking a checkbox radio, is mandatory to add to each one an actual ```value``` attribute**

This means that when that radio button is the selected option, send ```colors``` = ```value``` 

```html
<form action="http://www.google.com">
    <input type="radio" id="Red" name="colors" value="red">
    <label for="Red">Red</label>

    <input type="radio" id="Orange" name="colors" value="orange"> 
    <label for="Orange">Orange</label>
    
    <input type="radio" id="Blue" name="colors" value="blue">
    <label for="Blue">Blue</label>

    <input type="submit" value="go">
</form>
```

Result is:

```https://www.google.com/?colors=blue```

### Checkbox

Checkbox attributes:

* ```id```: required to match the value with the ```<label>```

* ```name```: required to specify which value is going to be sent in the request

* ```checked```: a boolean value that allows you to show the boxed as checked since from the start. 

```html
<label for="likeDogs">You like dogs?</label>
<input type="checkbox" name="likeDogs" id="likeDogs" value="yes">
```


### Textarea

It's not exactly an input type but it's a valid ```<form>``` element

```html
<textarea name="" id="" cols="100" rows="10">
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptate quidem sequi ipsam veniam illo voluptatibus illum em quam nihil eveniet.
</textarea>
```

### Select

```html
<select name="sort" id="sort">
    <option value="top">Top</option>
    <option value="new">New</option>
    <option value="relevance">Relevance</option>
</select>
```

### Validation

* ```required```

* ```maxlength=""```

*```minlength=""```


When needing to validate an input, you can add the ```required``` attribute. Required is a boolean value so it doesn't need any declaration.

```html
<input type="email" placeholder="email" required>
```

Can also validate content by using ```maxlength=""``` and the max value. Same with ```minlength=""```

```html
<form action="">
    <input type="text" placeholder="username" required minlength="4">
    <input type="email" placeholder="email" required>
    <button>Submit!</button>
</form>
```

# Day 5

<article>
<section>
<summary>
<details>
<aside>
<footer>
<header>
<main>
<nav>
<section>

## Semantic Markup

It's the idea about using html markup tags and elements for what they were actually created for and not for whatever I want

### Why is it important?

1. Serching Engines Optimization
2. Accessibilty
3. Maintainability 


1. ```<nav>``` element

The HTML ```<nav>``` element represents a section of a page whose purpose is to provide navigation links, either within the current document or to other documents. Common examples of navigation sections are menus, tables of contents, and indexes.


2. ```<header>```

The HTML ```<header>``` element represents introductory content, typically a group of introductory or navigational aids. It may contain some heading elements but also a logo, a search form, an author name, and other elements.


3. ```<footer>```

The HTML ```<footer>``` element represents a footer for its nearest sectioning content or sectioning root element. A footer typically contains information about the author of the section, copyright data or links to related documents.


4. ```<article>```

The HTML ```<article>``` element represents a self-contained composition in a document, page, application, or site, which is intended to be independently distributable or reusable (e.g., in syndication). Examples include: a forum post, a magazine or newspaper article, or a blog entry.


5. ```<section>```

The HTML ```<section>``` element represents a standalone section — which doesn't have a more specific semantic element to represent it — contained within an HTML document. Typically, but not always, sections have a heading.


6. ```<aside>```

The HTML ```<aside>``` element represents a portion of a document whose content is only indirectly related to the document's main content. Asides are frequently presented as sidebars or call-out boxes.


7. ```<main>```

The HTML ```<main>``` element represents the dominant content of the ```<body>``` of a document. The main content area consists of content that is directly related to or expands upon the central topic of a document, or the central functionality of an application.


# Day 6

## CSS

**CSS (Cascading Style Sheets)** is a declarative language that controls how webpages look in the browser. The browser applies CSS style declarations to selected elements to display them properly.


### Some Properties

1. ```display```

The display CSS property sets whether an element is treated as a block or inline element and the layout used for its children, such as flow layout, grid or flex.

[Display - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/display)


# Day 7

## CSS Selectors

General Patter:

```cs
selector {
    property: value;
}
```

1. Universal Selector ```*```:

Matches all and every element in the html and gives it the stablished property .

```css
* {
   color: red; 
}
```

2. Element/Type Selector:

Styles all the elements that match the given _type_:

```css
img {
    width: 100px;
    height: 200px;
}

a {
    color: pink;
}

h2 {
    font-size: 40px;
}
```

3. Class Selector

A class is a way of grouping elements together. Selects all the elements with the _class name_ assigned. The class must exist inside the HTML tag or section you want to style. 

```css
.icon {
    color: green;
}
```

4. ID Selector

As classes, is another way of adding a hook to a markup. It can only be assigned only once to only one element. They are unique.


```css
#idNameAssociated {
    font-family: sans-serif;
    heigh
}
```

5. Attribute Selector

Allows us to select elements based of the values of some attribute

[Attribute Selectors Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

```css
input[type="text"] {
    width: 300px;
    color: yellow;
}
```

6. Selector List

Is a way of styling multiple selectors at once. We use the "," to list the selectors. 


```css
h1, h2 {
    color:pink;
 }

#logo, img, .icon {
    font-size: 30px;
}

```

7. Child Combinator

It targets only the given selector that are a **direct** children of the selector assigned before.

```css
div > li {
    color: white;
}
```

8. Descendant Combinator

Let us target elements that are descendants of some other selectors

```css
li a {
    display: inline;
}
```

9. Pseudo Classes

Keyword added to a selector that specifies a **special state** of the selected element(s)

[Pseudo Classes Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

* ```:active```

```css

```

* ```:visited```

```css
a:visited {
    color: red;
}
```

* ```:hover```

```css
img:hover {
    border: 2px solid green;
}

ol .icon:hover { 
    color: purple;
}
```

* ```:nth-of-type()```

Matches elements of a given type, based on their position among a group of siblings.

Selects every fourth ```<p>``` element among any group of siblings

```css
p:nth-of-type(4n) {
  color: lime;
}
```

* ```:focus```

```css
input:focus {
    border: 1px solid magenta;
    outline: none;
}
```

10. Pseudo Elements

Keyword added to a selector that lets you **style a particular part** of selected elements.

[Pseudo-Elements Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)

* ```::after```

It is often used to add **cosmetic content to an element** with the content property. It is inline by default.

```css
/* Add double bar after links */
a::after {
    content: "||"
}
```

* ```::before```

It is often used to add **cosmetic content to an element** with the content property. It is inline by default.

```css
/* Add double bar after links */
a::before {
    content: "||"
}
```

* ```::first-letter```

```css
h2::first-letter {
    font-size: 50px;
    color: olive;
}
```

* ```::selection```

Allows you to style any text that has been selected.

```css
::selection {
    background-color: cyan;
    color: white;
}
```


# DAY 8 - CSS Colors

# DAY 9 - The CSS Box Model

Every element in CSS has a box around it. Four main elements compose every CSS element

1. **Content Box**

2. **Padding**

3. **Border**

4. **Margin**

# DAY 10 - CSS Text Properties




# DAY 13 - Flexbox

There area two groups of properties:

### Container Properties

* Flex-direction

* Justify-content

* Flex-wrap

* Align-items

* Align-content


### Flex Item Properties

* Order

* Flex

* Flex-grow

* Flex-shrink

* Align-self


### Flex Container

**Main Axis**: by default is *from left to right*

**Cross Axis**: is perpendicular to Main-Axis and it goes by default *from top to bottom*


### Container Properties

1. **flex-directon**: specifies how items are placed in the flex container, defining the *main axis* and its *direction*. The default is ```flex-direction: row;```. Now, the main axis goes *from right to left*. Othe possible values:
    
    * ```row-reverse```: 

    * ```column```: main axis switches from *top to bottom* and cross axis from *left to right*

    * ```column-reverse``` main axis switches from *bottom to top*

2. **flex-wrap**: specifies whether items in a flexbox or flex container are forced into a single line OR can be wrapped into multiple lines.  

    * ```wrap```: elements wrap into the container in case they don't fit.

    * ```wrap-reverse```: this alters the direction of the cross axis from bottom to top. So the wrapping now is not gonna be downward but upward.

3. **justify-content**: defines *how space is distributed between items in flex container **along the main axis***.

    * ```flex-start```
    
    * ```flex-end```
    
    * ```center```
    
    * ```space-around```

    * ```space-between```

    * ```evenly```

4. **align-items**: defines *how space is distributed between items in flex container **along the cross axis***.

    * ```flex-start```
    
    * ```flex-end```
    
    * ```center```
    
    * ```space-around```

    * ```space-between```

    * ```stretch```: the content stretches to fit the cross axis

    * ```baseline```


5. **align-content**: defines how space is distributed **between rows** in flex container **along the cross axis**. Align-content is for multi line flexible boxes. It has no effect when items are in a single line. It aligns the whole structure according to its value

    * ```center```

    * and more


### Flex items properties:

Properties that you apply to the individual items that are inside 

1. ```align-self```: allows us to override align-items on individual flex items.

2. ```flex```: defines how a flex item will grow or shrink to fit the available space in a container. It's a shorthand property for 3 other properties: ```flex-grow```, ```flex-shrink```, ```flex-basis```

    * ```flex-basis```: specifies the initial ideal size of a flex item **BEFORE** it's placed into a flex container. Ej.: ```flex-basis: 200px;``` or ```flex-basis: 25%;```. If they are in a row, they will take 25% of the space horizontally (width); if they are in a column, they will take 25% of the space vertically (height). But if they can't wrap or there are too many elements then they will have to shrink.   

    * ```flex-shrink```: dictates how items should shrink when there isn't enough space in container. The units are based on ratios units. Ej.: ```flex-shrink: 2;``` 

    * ```flex-grow```: dictates how the unused space should be spread amongst flex items. The units are based on ratios units. Ej.: ```flex-grow: 2;```

**```flex```: flex-grow | flex-shrink | flex-basis**

3. ```order```: specifies the order used to lay out items in their flex container. i.e.: ```order: 1```
All items by default have an order of 0


# DAY 10 - Text Properties


Measurment units: 

* _px_
* _%_
* _em_
* _rem_ (root em's)
* _vh_ (viewport height)
* _vw_ (viewport width)
* _x-small_

1. ```font-size```

If you set a ```font-size``` for a parent and the children doesn't have a ```font-size``` set, it will inherit from it's parent

```css
font-size: 40px;
```


2. ```font-family```



3. ```font-weight```

Sets the weight or boldness of the font. The weights depend on the ```font-family```. 

Normal weight is ```400```; ```700``` is bold weight. 

```css
font-weight: 700; /* or ```bold``` */
```

4. ```font-style```

Sets _italic_ font or non-italic font. Also you can set font-style to ```oblique```

5. ```text-transform```



6. ```text-decoration```



7. ```text-shadow```



8. ```text-align```

Sets horizontal alignment of a **block element**. Works like ```vertical-align``` but in the horizontal direction. 

```css
text-align: left;
```
Other values: ```left```, ```right```, ```center```, ```justify```, ```justify-all```, ```end```, ```start```


9. ```line-height```



10. ```letter-spacing```



11. ```letter-spacing```



12. ```text-overflow```