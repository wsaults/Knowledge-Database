#HTML/CSS Notes:

> Note: A collection of notes from the [teamtreehouse.com](teamtreehouse.com) web path.



##Intro to HTML and CSS

[placeimg](http://placeimg.com/)

```<a href="#top"></a>```#top in an anchor tag takes you to the top of the page

```<a href="#"></a>``` also takes you to the top of the page

```<a href="#" target="_blank"></a>``` target _blank opens a new tab



###CSS

```:hover``` /* designates a hover state */

class name convention resembles "card-title"

[CSS-TRICKS](www.css-tricks.com/almanac)

Padding: the space between an element and its border. Changes the space inside an element's box

Margin: the space outside an element's border. Changes the space outside an element's box



###HTML Documents

doctype: ```<!DOCTYPE html>```

Link stylesheet ```<link rel="stylesheet" href="styles.css">```



------

#HTML Basics Notes:

## Common html tags used for semantics:

- header
- footer
- section (groups related content)
- article (describes self containted content)
- nav
- aside (side bar)



HTML character entity for copyright: ```&copy;```

```<q>``` is used to add quotes.

Use ```<blockquote cite="www.nothing.com">``` To indicate quoting someone. You can also use ```<cite>``` inline with a anchor tag to the resource.

```<footer>``` and ```<header>``` can be added to sub tags 



## Images

```<img>``` attributes are ```src```, ```alt```, and ```title```

The ```<figure>``` and ```<figcaption>``` tags help to set aside image content by intenting and adding the ```<figcaption>``` text below the image.



```<address>``` represents contact information for a person.



## Text level elements

- ```<hr>``` Creates a vertical separation and a line
- ```<br>``` Adds vertical break between text
- ```<strong>``` Adds bold to text
- ```<em>``` Adds italics to text
- ```<small>``` For disclaimers and copyright info
- ```<span>``` Group text for styling



## Linking to sections of a webpage

Set the href of an anchor tag to the id of an element.

```/``` Start the root relative path.



### Launching an email composer

```<a href="mailto:test@example.com?subject="Some%20subject">test@example.com</a>```



### Entity references

[Character entity chart](https://dev.w3.org/html5/html-author/charref)



## Web design process

1. Define goals
2. Realize audience
3. Gather content




## CSS

[CSS-Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)

[WebPlatform](https://www.webplatform.org/docs/css/)

[CanIUse](http://www.caniuse.com)

[CSS Data types](https://developer.mozilla.org/en-US/docs/tag/CSS%20Data%20Type)

####Linking a stylesheet

`<link rel="stylesheet" href="css/style.css">`



####Import a stylesheet

At the top of a css file use

`@import "imports-styles.css";`



### Styles

#####Universal selector

`* {}`

#####Type/Element selectors

ex: `p, h1, a, div`

#####ID selectors

`#name {}`

#####Class selectors

`.name {}`

#####Descendant selectors

`parent-selector child-selector {}`

`parent-class-selector child-selector {}`

ex: `ul li {}`

##### Pseudo-Classes

ex: `a:link {}`

ex: `a:hover {}`

##### Comments

`/* */`



### Units of measurement

#### em

The em is known as a font-relative unit because it's calculated based on a parent element's font size.

#### rem

The difference is that rem is relative only to the root element of the page.



### Color values

#### Hex

\#ff0088

#### RGB

rgb(255, 255, 255)

#### RGBA

rgba(255, 255, 255, .9)



### Font

#### Font one-liner

`font: normal 1em/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif;`



## CSS Box Model

#### Border style

Border examples:

`boder: 10px solid red`

`border: solid dotted 10px 20px red white`

#### Display

`none, block, inline, inline-block `



## Floats

Clearing floats:

`overflow: auto;`

```
.group:after {
	content: "";
	display: table;
	clear: both:
}
```



##Lists

`list-style-type: square;`



## Text shadows

Horizontal offset, Vertical offset, Blur offset, Color

`text-shadow: 5px 8px 0 #222;`



##Box shadow

X, Y, blur radius, spread distance

may add inset as first value

`box-shadow: 15px 15px rgba(0,0,0, .8);`



## Border radius

`border-top-left-radius: 50px;`

`border-radius: 10px 5px;`



## Gradients

###Linear

`background-image: linear-gradient(0deg, #000000, firebrick)`

### Radial

`background-image: radial-gradient(#000000, firebrick)`

#### Circle

`background-image: radial-gradient(circle, #000000, firebrick)`

`background-image: radial-gradient(circle at top right, #000000, firebrick)`

#### Color stops

`background-image: linear-gradient(#000000, firebrick 0%, dodgerblue 50%, white 100%)`

#### Transparent Gradients and Multiple BGs

```
background: linear-gradient(#ffa949, transparent 90%), 
		   #ffa949 url('img.jpg')no-repeat center;
```

```
background: linear-gradient(#ffa949, transparent 90%), 
		   linear-gradient(0deg, #fff, transparent),
            #ffa949 url('img.jpg')no-repeat center;
```



## Web fonts

`@font-face { font-family: 'Abolition Regular' src: url(font.ttf); }`



##Media Queries

Media types: all (default), print, screen, speech

```
@media all (max-width: 960px)  {
	body { properties... } 
}
```

####Compound queries
```
@media all (max-width: 960px) and (max-width:700px) {
	body { properties... } 
}
```
`<meta name = "viewport" content="width=device-width">`



## Cascade

- Importance (User agent, User, Author)
- Specificity
- Sort order





# CSS Selectors



## Attribute selectors

  ```
[class="form-contact"] {
  color: red;
}
  ```

Target a form element:

```
form[class="form-contact"] {
  color: red;
}
```

Tartget a div with an id

```
div[id="containter"] {
  color: red;
}
```

Target specific input fields without using a class or id

```
input[type="text"] {
  color: red;
}
```



### Child, adjacent, and general sibling combinators

####Direct child selector:

```
form > a {
}
```

#### Adjacent sibling selector

```
.btn + .btn {
}
```

#### General sibling selector (All following siblings)

```
h1 ~ label {}
```



#### :first-child and :last-child

```
li:first-child {}
li:last-child {}
```



#### :only-child and :empty

```
span:only-child {}
```

```
li:empty {}
```



### Begins with and ends with

#### Begins with

```
a[href^="http://"] {}
```

#### Ends with

```
a[href$=".pdf"] {}
```

#### Any

```
a[href*="downloads"] {}
```



### :nth-child

```
li:nth-child(even) {}
li:nth-child(3) {}
li:nth-child(2n+3) {} // an+b --- b selects a value then a skips that many repeatedly

li:nth-child(n+4) {} // 'a' can be ommited --- forth then every one after
li:nth-child(3n+0) {} // select ever other 3rd child (+0 can be ommited)

li:nth-child(-n+3) {} // Targets all elements 3 and prior
```



### :nth-of-type

```
div:nth-of-type(4) {} // targest the 4th div in the parent
div:nth-last-of-type() {}
```



### :root and :target

```
:root {} // Highest level partent
:target {} // Selects an element that is the target of a link
```



### :not()

```
div:not(#col-a) {} // Targets every element but the argument
.col:not(:first-child) {} // Targets all columns except the first
```



## Pseudo-Elements

### ::first-line and ::first-letter

```
.intro::first-line {}
p::first-letter {}
```



### ::before and ::after

```
.jpg::before {
  content: "JPG - ";
}
.jpg::before {
  content: url(img.png);
}
.a::after {
  content: "";
  display: inline-block;
  background: coral;
}
```



### attr() function

```
.d-loads a::after {
  content: attr(title); // instert the title element as the content
  display: inline-block;
  color: initial;
}
```



## CSS Display

- use normalize.css to remove default browser styles for better cross browser consistency.

- Use a layout wrapper or "container" to wrap the content.

  ```css
  // Add a div with class "wrapper" inside the body tag
  .wrapper {
      width: 70%;
      margin: 0 auto; // Top margin 0, center align content.
  }
  ```

- Use class = "container" around sections of content.

### Vertical margins collapse

- Set the top-margin of the offending element to 0 OR

- Give the top header element a padding value.

  ​

### Media queries

http://www.initializr.com/

```css
// Base element styles
* {
    box-sizing: border-box; // Forces the padding and borders into the width and height of the elements.
}

// Media queries
@media (min-width: 769px) {
    .container {
        max-width: 1000px;
    }
}

// Breakpoints
@media only screen and (min-width: 480px) {}
@media only screen and (min-width: 768px) {}
@media only screen and (min-width: 1140px) {}
```



### Creating a sticky footer

```css
// Wrap the header and content in a container
.wrap {
    min-height: calc(100vh - 89px); 
    // 100% of viewport-height - footer height
}
```



### Inline display

*note: block level elements appear stacked on top of each other.

```css
display: inline; 
// Causes elements to take up as much space as their content.
```



### Inline Block

The advantage to using inline-block over inline display is that you can style inline-block elements as you would block-level elements. You can apply a width, height, and top/bottom margins and padding.



### Absolute Positioning

```css
.example {
    position: absolute;
    top: 0px;
    left: 0px;
}
```

- Elements with absolute positioning are neither affected by or do not affect other elements in the normal flow of the page.
- They are like layers in Photoshop or Illustrator; you're free to place them anywhere you wish on the page.
- Positioned elements rely on you telling the browser where to place them, using values called positioning offsets, for the element's top, right, bottom or left position.
- When you use absolute positioning, you place the absolutely positioned elements in relation to a parent container; the parent container is the positioning context.
- You can change the positioning context to other containing elements; this lets us position elements precisely where we want them.



### Fixed Positioning

```css
.body {
    padding-top: 68px; // Compensate for the space covered by the header.
}

.main-header {
    position: fixed; // Does not affect the position of the other elements.
    width: 100%;
    top: 0; // Anchors to the top of the browser.
    z-index: 1000;
}
```

- Unlike absolute positioning, an element with fixed positioning stays fixed to one spot on the page, regardless of the size of the browser window.
- Fixed headers and navigation bars are common in web design. For example, the [navigation bar on Twitter](https://twitter.com/treehouse).
- Fixed positioning is always relative to the browser's viewport. Like absolute positioning, you determine the fixed spot using offset values.
- When you use relative, absolute or fixed positioning on elements, you may end up with several elements occupying the same space. This can make elements overlap or completely cover up other elements from view.




## Flexbox

- The two most important elements in flexbox layout are **flex containers** and **flex items**.
- The **flex container** sets the context for flexbox layout; it contains flex items, the actual elements you layout using flexbox.
- Every direct child of a flex container is called a **flex item**; there can be any number of flex items inside a flex container.
- Once the children are flex items, you can take advantage of flexbox's powerful alignment properties.
- Flexbox follows two axes that determine the layout direction of flex items: **main axis** and **cross axis**.
- The main axis is the primary axis along which flex items are laid out; it defines the direction of flex items in the flex container.
- The cross axis runs perpendicular to the main axis.
- Each axis has a start side and an end side.
- The default main-start and main-end direction of the main axis is left-to-right.
- The the default direction of the cross axis is top-to-bottom.




### Flex Direction

- Some flexbox properties apply to the flex container only, while some apply only to the flex items.
- The `flex-direction` property **applies to the flex container only**.
- The default value for `flex-direction` is `row`.
- To reverse the direction flex items in a row, use the value `row-reverse`.
- The value `column` rotates the main axis so that flex items are laid out vertically.
- Like the `row-reverse` property, you can swap the top-to-bottom direction of a column with the value `column-reverse`.

```css
flex-direction: row;
```



### Flex wrap

```css
flex-wrap: wrap;
```



### Justify content

```css
justify-content: flex-start;
```



### Flex grow

- The `flex-grow` property applies to **flex items only**.
- A `flex-grow` value of `1` expands flex items to take up the full space of a line.
- The higher the `flex-grow` value, the more an item grows relative to the other items.

```css
flex-grow: 1;
```

```css
// You set the initial size you want the flex items to be, then flexbox evenly distributes the free space according that size.

flex-basis: 200px;
```

```css
// Flex short hand
flex: 1; // Sets flex grow to 1
flex: 1 200px; // Adds flex-basis 200px 
```



## HTML Forms

```html
<form action="index.html" method="post">
</form>
```



### Input

```html
<input type="text" id="name" name="user_name"> // This is a self-closing tag.
```

### Textarea

```html
<textarea id="bio" name="user_bio"></textarea>
```

### Button

```html
<button type="submit">Sign up</button>
<button type="reset">Reset</button>
<button type="button">Some button</button>
```

### Label

```html
<label for="name">Name:</label> // Matches an input with the same id
<input id="name">
```

### Fieldset and legend

```html
<form>
    <fieldset>
        <legend>Info</legend>
        ...
    </fieldset>
    
    <fieldset>
        <legend>Other</legend>
        ...
    </fieldset>
</form>

```

### Select Menus

```html
<select id="job" name="user_job">
    <optgroup label="Web">
        <option value="frontend_developer">Front-End Developer</option>
        <option value="php_developer">PHP Developer</option>
        <option value="python_developer">Python Developer</option>
    	<option value="rails_developer">Rails Developer</option>
    	<option value="web_designer">Web Designer</option>
    </optgroup>
    <optgroup label="Mobile">
        <option value="ios_developer">iOS Developer</option>
    </optgroup>
</select>


```

### Radio Buttons

```html
<label>Age:</label> // Doesn't need a for attribute
<input type="radio" id="under_13" value="under_13" name="user_age" class="light">
<label for="under_13">Under 13</label>
<br>
<input type="radio" id="over_13" value="over_13" name="user_age" class="light"> // Having the same name keep the radios grouped to allow only one selection 
<label for="over_13">Over 13</label>
```

### Checkboxes

```html
<label>Interests</label>
<input type="checkbox" id="development" value="interest_development" name="user_interest">
<label class="light" for="development">Development</label><br>

<input type="checkbox" id="design" value="interest_design" name="user_interest">
<label class="light" for="design">Design</label>
```



## Jquery

```javascript
// Query selector
jquery('.box').hide();
$('.box').hide(); // The same as above.

// Click event
$('.box').click(function() {
   alert('Clicked!');
});
```

