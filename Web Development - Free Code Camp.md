# Applied Visual Design 

## Create a Gradual CSS Linear Gradient

Applying a color on HTML elements is not limited to one flat hue. CSS provides the ability to use color transitions, otherwise known as gradients, on elements. This is accessed through the ```background``` property's ```linear-gradient()``` function. Here is the general syntax:

```cs
background: linear-gradient(gradient_direction, color 1, color 2, color 3, ...);
```

The first argument specifies the direction from which color transition starts - it can be stated as a degree, where 90deg makes a vertical gradient and 45deg is angled like a backslash. The following arguments specify the ```order``` of colors used in the gradient.

Example:

```cs
background: linear-gradient(90deg, red, yellow, rgb(204, 204, 255));
```

The ```repeating-linear-gradient()``` function is very similar to ```linear-gradient()``` with the major difference that it repeats the specified gradient pattern.

Example:

```cs
background: repeating-linear-gradient(
      90deg,
      yellow 0px,
      blue 40px,
      green 40px,
      red 80px
    );
```

## Use the CSS Transform scale Property to Change the Size of an Element

To change the scale of an element, CSS has the ```transform``` property, along with its ```scale()``` function. The following code example doubles the size of all the paragraph elements on the page:

```cs
p {
  transform: scale(2);
}
```

## Use the CSS Transform scale Property to Scale an Element on Hover

The ```transform``` property has a variety of functions that let you scale, move, rotate, skew, etc., your elements. When used with pseudo-classes such as ```:hover``` that specify a certain state of an element, the transform property can easily add interactivity to your elements.

Here's an example to scale the paragraph elements to 2.1 times their original size when a user hovers over them:

```cs
p:hover {
  transform: scale(2.1);
}
```

Note: Applying a ```transform``` to a ```<div>``` element will also affect any child elements contained in the ```<div>```.

## Use the CSS Transform Property skewX to Skew an Element Along the X-Axis

The next function of the ```transform``` property is ```skewX()```, which skews the selected element along its X (horizontal) axis by a given degree.

The following code skews the paragraph element by -32 degrees along the X-axis.

```cs
p {
  transform: skewX(-32deg);
}
```

## Use the CSS Transform Property skewY to Skew an Element Along the Y-Axis

Given that the ```skewX()``` function skews the selected element along the X-axis by a given degree, it is no surprise that the ```skewY()``` property skews an element along the Y (vertical) axis.

```cs
#top {
    background-color: red;
    transform: skewY(-10deg);
  }
```

_Additional Note:_
>You may recall from an earlier challenge that the box-shadow property takes values for offset-x, offset-y, blur-radius, spread-radius and a color value in that ```order```. The blur-radius and spread-radius values are optional.


## ```::before``` & ```::after``` 

Need to understand the ```::before``` and ```::after``` pseudo-elements. **These pseudo-elements are used to add something before or after a selected element**. In the following example, a ```::before``` pseudo-element is used to add a rectangle to an element with the class ```heart```:

```cs
.heart::before {
  content: "";
  background-color: yellow;
  border-radius: 25%;
  position: absolute;
  height: 50px;
  width: 70px;
  top: -50px;
  left: 5px;
}
```

For the ```::before``` and ```::after``` pseudo-elements to function properly, they must have a defined ```content``` property. This property is usually used to add things like a photo or text to the selected element. When the ```::before``` and ```::after``` pseudo-elements are used to make shapes, the ```content``` property is still required, but it's set to an empty string (```""```). 

In the above example, the element with the class of ```heart``` has a ```::before``` pseudo-element that produces a yellow rectangle with ```height``` and ```width``` of 50px and 70px, respectively. This rectangle has round corners due to its 25% b```order``` radius and is positioned absolutely at 5px from the left and 50px above the top of the element.

## Animations with CSS @keyframes and animation Properties Work

[Animations W3School](https://www.w3schools.com/css/css3_animations.asp)

To animate an element, you need to know about the ```animation``` properties and the ```@keyframes``` rule. The animation properties control how the animation should behave and the ```@keyframes``` rule controls what happens during that animation. There are eight animation properties in total.

* ```animation-name``` sets the name of the animation, which is later used by ```@keyframes``` to tell CSS which rules go with which animations.

* ```animation-duration``` sets the length of time for the animation.

* ```@keyframes``` is how to specify exactly what happens within the animation over the duration. This is done by giving CSS properties for specific "frames" during the animation, with percentages ranging from 0% to 100%. If you compare this to a movie, the CSS properties for 0% is how the element displays in the opening scene. The CSS properties for 100% is how the element appears at the end, right before the credits roll. Then CSS applies the magic to transition the element over the given duration to act out the scene. Here's an example to illustrate the usage of ```@keyframes``` and the animation properties:

```cs
#anim {
  animation-name: colorful;
  animation-duration: 3s;
}

@keyframes colorful {
  0% {
    background-color: blue;
  }
  100% {
    background-color: yellow;
  }
}
```

For the element with the ```anim``` id, the code snippet above sets the ```animation-name``` to ```colorful``` and sets the ```animation-duration``` to 3 seconds. Then the ```@keyframes``` rule links to the animation properties with the name ```colorful```. It sets the color to ```blue``` at the beginning of the animation (0%) which will transition to yellow by the end of the animation (100%). You aren't limited to only beginning-end transitions, you can set properties for the element for any percentage between 0% and 100%.

### Use CSS Animation to Change the Hover State of a Button

You can use CSS ```@keyframes``` to change the color of a button in its hover state.

Here's an example of changing the width of an image on hover:

```cs
<style>
  img:hover {
    animation-name: width;
    animation-duration: 500ms;
  }

  @keyframes width {
    100% {
      width: 40px;
    }
  }
</style>

<img src="https://bit.ly/smallgooglelogo" alt="Google's Logo" />
```

Example 2:

```html
<style>
  button {
    b```order```-radius: 5px;
    color: white;
    background-color: #0F5897;
    padding: 5px 10px 8px 10px;
  }

  button:hover {
    animation-name: background-color;
    animation-duration: 500ms;
  }

  @keyframes background-color {
    100% {
      background-color: #4791d0;
    }
  }

</style>

<button>Register</button>
```


Note that ms stands for milliseconds, where 1000ms is equal to 1s.

### Fill Mode of an Animation

Notice how the animation resets after ```500ms``` has passed, causing the button to revert back to the original color. You want the button to stay highlighted.

This can be done by setting the ```animation-fill-mode``` property to ```forwards```. **The ```animation-fill-mode``` specifies the style applied to an element when the animation has finished**. You can set it like so:


```animation-fill-mode: forwards;```

### Create Movement Using CSS Animation

When elements have a specified ```position```, such as ```fixed``` or ```relative```, the CSS offset properties ```right```, ```left```, ```top```, and ```bottom``` can be used in animation rules to create movement.

As shown in the example below, you can push the item downwards then upwards by setting the ```top``` property of the ```50%``` keyframe to 50px, but having it set to 0px for the first (0%) and the last (100%) keyframe.

```cs
@keyframes rainbow {
  0% {
    background-color: blue;
    top: 0px;
  }
  50% {
    background-color: green;
    top: 50px;
  }
  100% {
    background-color: yellow;
    top: 0px;
  }
}
```

### Animate Elements Continually Using an Infinite Animation Count

Another animation property is the animation-iteration-count, which allows you to control how many times you would like to loop through the animation. Here's an example:

```animation-iteration-count: 3;```

In this case the animation will stop after running 3 times, but it's possible to make the animation run continuously by setting that value to ```infinite```.

```html
<style>
  .back {
    position: fixed;
    padding: 0;
    margin: 0;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: white;
    animation-name: backdiv;
    animation-duration: 1s;
    animation-iteration-count: infinite;

  }

  .heart {
    position: absolute;
    margin: auto;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: pink;
    height: 50px;
    width: 50px;
    transform: rotate(-45deg);
    animation-name: beat;
    animation-duration: 1s;
    animation-iteration-count: infinite;

  }
  .heart:after {
    background-color: pink;
    content: "";
    b```order```-radius: 50%;
    position: absolute;
    width: 50px;
    height: 50px;
    top: 0px;
    left: 25px;
  }
  .heart:before {
    background-color: pink;
    content: "";
    b```order```-radius: 50%;
    position: absolute;
    width: 50px;
    height: 50px;
    top: -25px;
    left: 0px;
  }

  @keyframes backdiv {
    50% {
      background: #ffe6f2;
    }
  }

  @keyframes beat {
    0% {
      transform: scale(1) rotate(-45deg);
    }
    50% {
      transform: scale(0.6) rotate(-45deg);
    }
  }

</style>
<div class="back"></div>
<div class="heart"></div>
```

### Animate Multiple Elements at Variable Rates

Change the animation rates for two similarly animated elements by altering their ```@keyframes``` rules. You can achieve the same goal by manipulating the ```animation-duration``` of multiple elements.

To make change the rates, you can set the ```animation-duration``` property to different values for each element.

### Change Animation Timing with Keywords

In CSS animations, the ```animation-timing-function``` property controls how quickly an animated element changes over the duration of the animation. If the animation is a car moving from point A to point B in a given time (your ```animation-duration```), the ```animation-timing-function``` says how the car accelerates and decelerates over the course of the drive.

There are a number of predefined keywords available for popular options. For example, the default value is ```ease```, which starts slow, speeds up in the middle, and then slows down again in the end. Other options include ```ease-out```, which is quick in the beginning then slows down, ```ease-in```, which is slow in the beginning, then speeds up at the end, or ```linear```, which applies a constant animation speed throughout.

### How Bezier Curves Work

CSS offers an option other than keywords that provides even finer control over how the animation plays out, through the use of Bezier curves.

In CSS animations, Bezier curves are used with the ```cubic-bezier``` function. The shape of the curve represents how the animation plays out. The curve lives on a 1 by 1 coordinate system. The X-axis of this coordinate system is the duration of the animation (think of it as a time scale), and the Y-axis is the change in the animation.

The ```cubic-bezier``` function consists of four main points that sit on this 1 by 1 grid: ```p0```, ```p1```, ```p2```, and ```p3```. ```p0``` and ```p3``` are set for you - they are the beginning and end points which are always located respectively at the origin (0, 0) and (1, 1). You set the x and y values for the other two points, and where you place them in the grid dictates the shape of the curve for the animation to follow. This is done in CSS by declaring the x and y values of the ```p1``` and ```p2``` "anchor" points in the form: (x1, y1, x2, y2). Pulling it all together, here's an example of a Bezier curve in CSS code:

```
animation-timing-function: cubic-bezier(0.25, 0.25, 0.75, 0.75);
```

In the example above, the x and y values are equivalent for each point (x1 = 0.25 = y1 and x2 = 0.75 = y2), which if you remember from geometry class, results in a line that extends from the origin to point (1, 1). This animation is a linear change of an element during the length of an animation, and is the same as using the linear keyword. In other words, it changes at a constant speed.

### Use a Bezier Curve to Move a Graphic

Similar animation progressions to the ```ease-out``` keyword can be achieved by using a custom cubic Bezier curve function.

In general, changing the ```p1``` and ```p2``` anchor points drives the creation of different Bezier curves, which controls how the animation progresses through time. Here's an example of a Bezier curve using values to mimic the ```ease-out``` style:

```
animation-timing-function: cubic-bezier(0, 0, 0.58, 1);
```

Remember that all cubic-bezier functions start with ```p0``` at (0, 0) and end with ```p3``` at (1, 1). In this example, the curve moves faster through the Y-axis (starts at 0, goes to p1 y value of 0, then goes to p2 y value of 1) than it moves through the X-axis (0 to start, then 0 for ```p1```, up to 0.58 for ```p2```). 

As a result, the change in the animated element progresses faster than the time of the animation for that segment. Towards the end of the curve, the relationship between the change in x and y values reverses - the y value moves from 1 to 1 (no change), and the x values move from 0.58 to 1, making the animation changes progress slower compared to the animation duration.

### Make Motion More Natural Using a Bezier Curve

This challenge animates an element to replicate the movement of a ball being juggled.

The ```animation-timing-function``` automatically loops at every keyframe when the ```animation-iteration-count``` is set to ```infinite```. Since there is a keyframe rule set in the middle of the animation duration (at 50%), it results in two identical animation progressions at the upward and downward movement of the ball.

The following cubic Bezier curve simulates a juggling movement:

```cubic-bezier(0.3, 0.4, 0.5, 1.6);```

Notice that the value of y2 is larger than 1. Although the cubic Bezier curve is mapped on a 1 by 1 coordinate system, and it can only accept x values from 0 to 1, the y value can be set to numbers larger than one. This results in a bouncing movement that is ideal for simulating the juggling ball.

# Applied Accessibility

## Add a Text Alternative to Images for Visually Impaired 

```Alt``` text describes the content of the image and provides a text-alternative for it. This helps in cases where the image fails to load or can't be seen by a user. It's also used by search engines to understand what an image contains to include it in search results. Here's an example:

```html
<img src="importantLogo.jpeg" alt="Company logo">
```

People with visual impairments rely on screen readers to convert web content to an audio interface. They won't get information if it's only presented visually. For images, screen readers can access the ```alt``` attribute and read its contents to deliver key information.

Good ```alt``` text provides the reader a brief description of the image. You should always include an ```alt``` attribute on your image. Per HTML5 specification, this is now considered mandatory.

## Know When Alt Text Should be Left Blank
Sometimes images are grouped with a caption already describing them, or are used for decoration only. In these cases ```alt``` text may seem redundant or unnecessary.

In situations when an image is already explained with text content, or does not add meaning to a page, the ```img``` still needs an ```alt``` attribute, but it can be set to an empty string. Here's an example:

```html
<img src="visualDecoration.jpeg" alt="">
```

Background images usually fall under the 'decorative' label as well. However, they are typically applied with CSS rules, and therefore not part of the markup screen readers process.

_Addtional Note:_
>For images with a caption, you may still want to include ```alt``` text, since it helps search engines catalog the content of the image.
<hr>

>Semantic meaning means that the tag you use around content indicates the type of information it contains.

## Improve Accessibility of Audio Content with the audio Element

HTML5's audio element gives semantic meaning when it wraps sound or audio stream content in your markup. Audio content also needs a text alternative to be accessible to people who are deaf or hard of hearing. This can be done with nearby text on the page or a link to a transcript.

The ```audio``` tag supports the ```controls``` attribute. This shows the browser default play, pause, and other controls, and supports keyboard functionality. This is a boolean attribute, meaning it doesn't need a value, its presence on the tag turns the setting on.

Here's an example:

```html
<audio id="meowClip" controls>
  <source src="audio/meow.mp3" type="audio/mpeg" />
  <source src="audio/meow.ogg" type="audio/ogg" />
</audio>
```

_Additional Note:_ 
>Multimedia content usually has both visual and auditory components. It needs synchronized captions and a transcript so users with visual and/or auditory impairments can access it. Generally, a web developer is not responsible for creating the captions or transcript, but needs to know to include them.

## Use ```tabindex``` to Add Keyboard Focus to an Element

The HTML ```tabindex``` attribute has three distinct functions relating to an element's keyboard focus. When it's on a tag, it indicates that element can be focused on. The value (an integer that's positive, negative, or zero) determines the behavior.

Certain elements, such as links and form controls, automatically receive keyboard focus when a user tabs through a page. It's in the same ```order``` as the elements come in the HTML source markup. This same functionality can be given to other elements, such as ```div```, ```span```, and ```p```, by placing a ```tabindex="0"``` attribute on them. Here's an example:

```html
<div ```tabindex```="0">I need keyboard focus!</div>
```

_Additional Note:_ 
>A negative ```tabindex``` value (typically -1) indicates that an element is focusable, but is not reachable by the keyboard. This method is generally used to bring focus to content programmatically (like when a ```div``` used for a pop-up window is activated), and is beyond the scope of these challenges.

The ```tabindex``` attribute also specifies the exact tab ```order``` of elements. This is achieved when the value of the attribute is set to a positive number of 1 or higher.

Setting a ```tabindex="1"``` will bring keyboard focus to that element first. Then it cycles through the sequence of specified tabindex values (2, 3, etc.), before moving to default and ```tabindex="0"``` items.

Here's an example:

```html
<div tabindex="1">I get keyboard focus, and I get it first!</div>

<div tabindex="2">I get keyboard focus, and I get it second!</div>
```

# Responsive Web Design Principles 

## Create a Media Query

Media Queries are a new technique introduced in CSS3 that change the presentation of content based on different **viewport** sizes. **The viewport is a user's visible area of a web page, and is different depending on the device used to access the site.**

**Media Queries consist of a media type, and if that media type matches the type of device the document is displayed on, the styles are applied**.

Here's an example of a media query that returns the content when the device's **width** is less than or equal to 100px:

```css
@media (max-width: 100px) { /* CSS Rules */ }
```

The following media query returns the content when the device's **height** is more than or equal to 350px:

```css
@media (min-height: 350px) { /* CSS Rules */ }
```

Remember, the CSS inside the media query is applied only if the media type matches that of the device being used.

## Make an Image Responsive
Making images responsive with CSS is actually very simple. You just need to add these properties to an image:

```css
img {
  max-width: 100%;
  height: auto;
}
```

**IMPORTANT!**

The ```max-width``` of ```100%``` will make sure the image is never wider than the container it is in, and the height of ```auto``` will make the image keep its original aspect ratio.


## Use a Retina Image for Higher Resolution Displays

Pixel density is an aspect that could be different on one device from others and this density is known as Pixel Per Inch(PPI) or Dots Per Inch(DPI). The most famous such display is the one known as a "Retina Display" on the latest Apple MacBook Pro notebooks, and recently iMac computers. Due to the difference in pixel density between a "Retina" and "Non-Retina" displays, some images that have not been made with a High-Resolution Display in mind could look "pixelated" when rendered on a High-Resolution display.

The simplest way to make your images properly appear on High-Resolution Displays, such as the MacBook Pros "retina display" is to define their width and height values as only half of what the original file is. Here is an example of an image that is only using half of the original height and width:

```html
<style>
  img { height: 250px; width: 250px; }
</style>
<img src="coolPic500x500" alt="A most excellent picture">
```

## Make Typography Responsive

Instead of using ```em``` or ```px``` to size text, you can use ```viewport units``` for responsive typography. **Viewport units, like percentages, are relative units, but they are based off different items. Viewport units are relative to the viewport dimensions (width or height) of a device, and percentages are relative to the size of the parent container element.**

The four different viewport units are:

1. **vw (viewport width)**: 10vw would be 10% of the viewport's width.
2. **vh (viewport height)**: 3vh would be 3% of the viewport's height.
3. **vmin (viewport minimum)**: 70vmin would be 70% of the viewport's smaller dimension (height or width).
4. **vmax (viewport maximum)**: 100vmax would be 100% of the viewport's bigger dimension (height or width).

Here is an example that sets a body tag to 30% of the viewport's width.

```css
body { width: 30vw; }
```

# CSS Flexbox: Use display

## ```flex``` to Position Two Boxes

This section uses alternating challenge styles to show how to use CSS to position elements in a flexible way. First, a challenge will explain theory, then a practical challenge using a simple tweet component will apply the flexbox concept.

Placing the CSS property display: flex; on an element allows you to use other flex properties to build a responsive page.


## Add Flex Superpowers to the Tweet Embed

To the right is the tweet embed that will be used as the practical example. Some of the elements would look better with a different layout. The last challenge demonstrated ```display: flex```. Here you'll add it to several components in the tweet embed to start adjusting their positioning.

## Use the ```flex-direction``` Property to Make a Row

**Adding ```display: flex``` to an element turns it into a flex container**. This makes it possible to align any children of that element into rows or columns. You do this by adding the ```flex-direction``` property to the parent item and setting it to row or column. Creating a row will align the children horizontally, and creating a column will align the children vertically.

Other options for ```flex-direction``` are ```row-reverse``` and ```column-reverse```.

Note: The default value for the ```flex-direction``` property is row.

## Align Elements Using the ```justify-content``` 

Sometimes the flex items within a flex container do not fill all the space in the container. It is common to want to tell CSS how to align and space out the flex items a certain way. Fortunately, the ```justify-content``` property has several options to do this. But first, there is some important terminology to understand before reviewing those options.

[Here is a useful image showing a row to illustrate the concepts below.](https://www.w3.org/TR/css-flexbox-1/images/flex-direction-terms.svg)

Recall that setting a flex container as a row places the flex items side-by-side from left-to-right. A flex container set as a column places the flex items in a vertical stack from top-to-bottom. For each, the direction the flex items are arranged is called the main axis. For a row, this is a horizontal line that cuts through each item. And for a column, the main axis is a vertical line through the items.

There are several options for how to space the flex items along the line that is the main axis. One of the most commonly used is ```justify-content: center;```, which aligns all the flex items to the center inside the flex container. Others options include:

1. ```flex-start```: aligns items to the start of the flex container. For a row, this pushes the items to the left of the container. For a column, this pushes the items to the top of the container. This is the default alignment if no ```justify-content``` is specified.

2. ```flex-end```: aligns items to the end of the flex container. For a row, this pushes the items to the right of the container. For a column, this pushes the items to the bottom of the container.

3. ```space-between```: aligns items to the center of the main axis, with extra space placed between the items. The first and last items are pushed to the very edge of the flex container. For example, in a row the first item is against the left side of the container, the last item is against the right side of the container, then the remaining space is distributed evenly among the other items.

4. ```space-around```: similar to ```space-between``` but the first and last items are not locked to the edges of the container, the space is distributed around all the items with a half space on either end of the flex container.

5. ```space-evenly```: Distributes space evenly between the flex items with a full space at either end of the flex container

## Align Elements Using the ```align-items``` Property

The ```align-items``` property is similar to ```justify-content```. Recall that the ```justify-content``` property aligned flex items along the main axis. For rows, the main axis is a horizontal line and for columns it is a vertical line.

Flex containers also have a cross axis which is the opposite of the main axis. For rows, the cross axis is vertical and for columns, the cross axis is horizontal.

CSS offers the ```align-items``` property to align flex items along the cross axis. For a row, it tells CSS how to push the items in the entire row up or down within the container. And for a column, how to push all the items left or right within the container.

The different values available for ```align-items``` include:

1. ```flex-start```: aligns items to the start of the flex container. For rows, this aligns items to the top of the container. For columns, this aligns items to the left of the container.

2. ```flex-end```: aligns items to the end of the flex container. For rows, this aligns items to the bottom of the container. For columns, this aligns items to the right of the container.

3. ```center```: align items to the center. For rows, this vertically aligns items (equal space above and below the items). For columns, this horizontally aligns them (equal space to the left and right of the items).

4. ```stretch```: stretch the items to fill the flex container. For example, rows items are stretched to fill the flex container top-to-bottom. This is the default value if no ```align-items``` value is specified.

5. ```baseline```: align items to their baselines. Baseline is a text concept, think of it as the line that the letters sit on.

## Use the ```flex-wrap``` Property to Wrap a Row or Column

CSS flexbox has a feature to split a flex item into multiple rows (or columns). By default, a flex container will fit all flex items together. For example, a row will all be on one line.

However, using the ```flex-wrap``` property tells CSS to wrap items. This means extra items move into a new row or column. The break point of where the wrapping happens depends on the size of the items and the size of the container.

CSS also has options for the direction of the wrap:

1. ```nowrap```: this is the default setting, and does not wrap items.

2. ```wrap```: wraps items from left-to-right if they are in a row, or top-to-bottom if they are in a column.

3. ```wrap-reverse```: wraps items from right-to-left if they are in a row, or bottom-to-top if they are in a column.

## Use the ```flex-shrink``` Property to Shrink Items
So far, all the properties in the challenges apply to the flex container (the parent of the flex items). However, there are several useful properties for the flex items.

The first is the ```flex-shrink``` property. When it's used, it allows an item to shrink if the flex container is too small. Items shrink when the width of the parent container is smaller than the combined widths of all the flex items within it.

The ```flex-shrink``` property takes numbers as values. The higher the number, the more it will shrink compared to the other items in the container. For example, if one item has a ```flex-shrink``` value of 1 and the other has a ```flex-shrink``` value of 3, the one with the value of 3 will shrink three times as much as the other.

## Use the ```flex-grow``` Property to Expand Items

The opposite of ```flex-shrink``` is the ```flex-grow``` property. Recall that ```flex-shrink``` controls the size of the items when the container shrinks. The ```flex-grow``` property controls the size of items when the parent container expands.

Using a similar example from the last challenge, if one item has a ```flex-grow``` value of 1 and the other has a ```flex-grow``` value of 3, the one with the value of 3 will grow three times as much as the other.

## Use the ```flex-basis``` Property to Set the Initial Size of an Item

The ```flex-basis``` property specifies the initial size of the item before CSS makes adjustments with ```flex-shrink``` or ```flex-grow```.

The units used by the ```flex-basis``` property are the same as other size properties (px, em, %, etc.). The value ```auto``` sizes items based on the content.

## Use the flex Shorthand Property

There is a shortcut available to set several flex properties at once. The ```flex-grow```, ```flex-shrink```, and ```flex-basis``` properties can all be set together by using the flex property.

**For example, ```flex: 1 0 10px```; will set the item to ```flex-grow: 1;```, ```flex-shrink: 0;```, and ```flex-basis: 10px;```.**

The default property settings are ```flex: 0 1 auto;```.

## Use the ```order``` Property to Rearrange Items

The ```order``` property is used to tell CSS the ```order``` of how flex items appear in the flex container. By default, items will appear in the same ```order``` they come in the source HTML. The property takes numbers as values, and negative numbers can be used.


**IMPORTANT!**

## Use the ```align-self``` Property

The final property for flex items is ```align-self```. This property allows you to adjust each item's alignment individually, instead of setting them all at once. This is useful since other common adjustment techniques using the CSS properties float, clear, and vertical-align do not work on flex items.

```align-self``` accepts the same values as align-items and will override any value set by the align-items property.



# CSS Grid

## Create Your First CSS Grid

Turn any HTML element into a grid container by setting its ```display``` property to ```grid```. This gives you the ability to use all the other properties associated with CSS Grid.

Note: In CSS Grid, the parent element is referred to as the _container_ and its children are called _items_.

## Add Columns with ```grid-template-columns```

Simply creating a grid element doesn't get you very far. You need to define the structure of the grid as well. To add some columns to the grid, use the ```grid-template-columns``` property on a grid container as demonstrated below:

```css
.container {
  display: grid;
  grid-template-columns: 50px 50px;
}
```

This will give your grid two columns that are each 50px wide. The number of parameters given to the ```grid-template-columns``` property indicates the number of columns in the grid, and the value of each parameter indicates the width of each column.

## Add Rows with ```grid-template-rows```

The grid you created in the last challenge will set the number of rows automatically. To adjust the rows manually, use the ```grid-template-rows``` property in the same way you used ```grid-template-columns``` in previous challenge.

## Use CSS Grid units to Change the Size of Columns and Rows

You can use absolute and relative units like ```px``` and ```em``` in CSS Grid to define the size of rows and columns. You can use these as well:

* ```fr```: sets the column or row to a fraction of the available space,

* ```auto```: sets the column or row to the width or height of its content automatically,

```%```: adjusts the column or row to the percent width of its container.

Here's the code that generates the output in the preview:

```grid-template-columns: auto 50px 10% 2fr 1fr;```

This snippet creates five columns. The first column is as wide as its content, the second column is 50px, the third column is 10% of its container, and for the last two columns; the remaining space is divided into three sections, two are allocated for the fourth column, and one for the fifth.

## Create a Column Gap Using ```grid-column-gap```

So far in the grids you have created, the columns have all been tight up against each other. Sometimes you want a gap in between the columns. To add a gap between the columns, use the ```grid-column-gap``` property like this:

```grid-column-gap: 10px;```

This creates 10px of empty space between all of our columns.

You can add a gap in between the rows of a grid using ``````grid-row```-gap``` in the same way that you added a gap in between columns.

## Add Gaps Faster with ```grid-gap```

```grid-gap``` is a shorthand property for ``````grid-row```-gap``` and ```grid-column-gap``` from the previous two challenges that's more convenient to use. If ```grid-gap``` has one value, it will create a gap between all rows and columns. However, if there are two values, it will use the first one to set the gap between the rows and the second value for the columns.

## Use ```grid-column``` to Control Spacing

Up to this point, all the properties that have been discussed are for grid containers. The ```grid-column``` property is the first one for use on the grid items themselves.

The hypothetical horizontal and vertical lines that create the grid are referred to as lines. These lines are numbered starting with 1 at the top left corner of the grid and move right for columns and down for rows, counting upward.

To control the amount of columns an item will consume, you can use the ```grid-column``` property in conjunction with the line numbers you want the item to start and stop at.

Here's an example:

```grid-column: 1 / 3;```

This will make the item start at the first vertical line of the grid on the left and span to the 3rd line of the grid, consuming two columns.

## Use ```grid-row``` to Control Spacing

Of course, you can make items consume multiple rows just like you can with columns. You define the horizontal lines you want an item to start and stop at using the ```grid-row``` property on a grid item.

## Align an Item Horizontally using ```justify-self```

In CSS Grid, the content of each item is located in a box which is referred to as a cell. You can align the content's position within its cell horizontally using the ```justify-self``` property on a grid item. By default, this property has a value of ```stretch```, which will make the content fill the whole width of the cell. This CSS Grid property accepts other values as well:

1. ```start```: aligns the content at the left of the cell,

2. ```center```: aligns the content in the center of the cell,

3. ```end```: aligns the content at the right of the cell.

## Align an Item Vertically using ```align-self```

Just as you can align an item horizontally, there's a way to align an item vertically as well. To do this, you use the ```align-self``` property on an item. This property accepts all of the same values as ```justify-self```.

## Align All Items Horizontally using ```justify-items```

Sometimes you want all the items in your CSS Grid to share the same alignment. You can use the previously learned properties and align them individually, or **you can align them all at once horizontally by using ```justify-items``` on your grid container**. This property can accept all the same values you learned about in the previous two challenges, the difference being that it will move all the items in our grid to the desired alignment.

Using the ```align-items``` property on a grid container will set the vertical alignment for all the items in our grid.

## Divide the Grid Into an Area Template

You can group cells of your grid together into an area and give the area a custom name. Do this by using ```grid-template-areas``` on the container like this:

```cs
grid-template-areas:
  "header header header"
  "advert content content"
  "footer footer footer";
```

The code above merges the top three cells together into an area named ```header```, the bottom three cells into a ```footer``` area, and it makes two areas in the middle row; ```advert``` and ```content```. 

Every word in the code represents a cell and every pair of quotation marks represent a row. In addition to custom labels, you can use a period (```.```) to designate an empty cell in the grid.

## Items in Grid Areas Using the ```grid-area``` Property

After creating an area's template for your grid container, as shown in the previous challenge, you can place an item in your custom area by referencing the name you gave it. To do this, you use the ```grid-area``` property on an item like this:

```css
.item1 {
  grid-area: header;
}
```

This lets the grid know that you want the ```item1``` class to go in the area named ```header```. In this case, the item will use the entire top row because that whole row is named as the header area.

## Use ```grid-area``` Without Creating an Areas Template

The ```grid-area``` property you learned in the last challenge can be used in another way. If your grid doesn't have an areas template to reference, you can create an area on the fly for an item to be placed like this:

```css
item1 { grid-area: 1/1/2/4; }
```

This is using the line numbers you learned about earlier to define where the area for this item will be. The numbers in the example above represent these values:

```
grid-area: horizontal line to start at / vertical line to start at / horizontal line to end at / vertical line to end at;
```
So the item in the example will consume the rows between lines 1 and 2, and the columns between lines 1 and 4.

## Reduce Repetition Using the ```repeat``` Function

When you used ```grid-template-columns``` and ```grid-template-rows``` to define the structure of a grid, you entered a value for each row or column you created.

Let's say you want a grid with 100 rows of the same height. It isn't very practical to insert 100 values individually. Fortunately, there's a better way - by using the ```repeat``` function to specify the number of times you want your column or row to be repeated, followed by a comma and the value you want to repeat.

Here's an example that would create the 100 row grid, each row at 50px tall.

```css
grid-template-rows: repeat(100, 50px);
```

You can also repeat multiple values with the repeat function and insert the function amongst other values when defining a grid structure. Here's what that looks like:

```css
grid-template-columns: repeat(2, 1fr 50px) 20px;
```

This translates to:

```css
grid-template-columns: 1fr 50px 1fr 50px 20px;
```

Note: The 1fr 50px is repeated twice followed by 20px.

## Limit Item Size Using the ```minmax``` Function

There's another built-in function to use with ```grid-template-columns``` and ```grid-template-rows``` called ```minmax```. It's used to limit the size of items when the grid container changes size. To do this you need to specify the acceptable size range for your item. Here is an example:

```css
grid-template-columns: 100px minmax(50px, 200px);
``` 

In the code above, ```grid-template-columns``` is set to create two columns; the first is 100px wide, and the second has the minimum width of 50px and the maximum width of 200px.

## Create Flexible Layouts Using ```auto-fill```

The ```repeat``` function comes with an option called ```auto-fill```. This allows you to automatically insert as many rows or columns of your desired size as possible depending on the size of the container. You can create flexible layouts when combining ```auto-fill``` with ```minmax```, like this:

```css
repeat(auto-fill, minmax(60px, 1fr));
```

When the container changes size, this setup keeps inserting 60px columns and stretching them until it can insert another one. Note: If your container can't fit all your items on one row, it will move them down to a new one.

## Create Flexible Layouts Using ```auto-fit```

```auto-fit``` works almost identically to ```auto-fill```. The only difference is that when the container's size exceeds the size of all the items combined, ```auto-fill``` keeps inserting empty rows or columns and pushes your items to the side, while ```auto-fit``` collapses those empty rows or columns and stretches your items to fit the size of the container.

Note: If your container can't fit all your items on one row, it will move them down to a new one.

## Use Media Queries to Create Responsive Layouts

CSS Grid can be an easy way to make your site more responsive by using media queries to rearrange grid areas, change dimensions of a grid, and rearrange the placement of items.

## Create Grids within Grids

Turning an element into a grid only affects the behavior of its direct descendants. So by turning a direct descendant into a grid, you have a grid within a grid.

For example, by setting the ```display``` and ```grid-template-columns``` properties of the element with the ```item3``` class, you create a grid within your grid.


[Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#flexbox-background)
