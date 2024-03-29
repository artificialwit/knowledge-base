## Cascading Style Sheets (CSS)

### CSS Selectors

CSS selectors are used to "find" (or select) the HTML elements you want to style.

We can divide CSS selectors into five categories:

- Simple selectors (select elements based on name, id, class)
- Combinator selectors (select elements based on a specific relationship between them)
- Pseudo-class selectors (select elements based on a certain state)
- Pseudo-elements selectors (select and style a part of an element)
- Attribute selectors (select elements based on an attribute or attribute value)

```css
// Element Selector
p {
  text-align: center;
  color: red;
}

// Id selector
#para1 {
  text-align: center;
  color: red;
}

// class selector
.center {
  text-align: center;
  color: red;
}

// Universal Selector - universal selector (*) selects all HTML elements on the page
* {
  text-align: center;
  color: blue;
}


// Grouping Selector - selects all the HTML elements with the same style definitions
h1, h2, p {
  text-align: center;
  color: red;
}

```

### Three Ways to Insert CSS

There are three ways of inserting a style sheet:

 - External CSS
  ```css
   <link rel="stylesheet" href="mystyle.css">
  ```
 - Internal CSS 
 ```html
 
 <style>
            body {
              background-color: linen;
            }

            h1 {
              color: maroon;
              margin-left: 40px;
            }
            </style>
 ````
 - Inline CSS
 
 ```html
 <h1 style="color:blue;text-align:center;">
```

### Color and background

```html
<html>
  <head> </head>
  <body>
    <style>
      h1 {
        color: white;
        text-align: center;
        font-size: 20px;
      }
      p {
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        font-size: 20px;
      }

      body {
        background-color: #ffffff;
        background-image: url("img_tree.png");
        background-repeat: no-repeat;
        background-position: right top;
      }
      /*Or*/
      body {
        background: #ffffff url("img_tree.png") no-repeat right top;
      }
    </style>
    <h1>FAI</h1>
    <h1 style="background-color: tomato;">Tomato</h1>
    <div>&nbsp</div>
    <h1 style="background-color: mediumseagreen;">mediumseagreen</h1>
    <div>&nbsp</div>
    <h1 style="background-color: lightgray; color: black;">lightgray</h1>
    <div>&nbsp</div>
    <h1 style="background-color: dodgerblue;">dodgerblue</h1>
    <div>&nbsp</div>
    <h1 style="background-color: orange;">orange</h1>
    <div>&nbsp</div>
    <h1 style="background-color: slateblue;">slateblue</h1>
    <h1 style="background-color: rgb(255, 99, 71, 0.4);">slateblue</h1>

    <h1 style="background-color: #3cb371;">slateblue</h1>

  </body>
</html>

```
### Borders and Outlines
- A border properties allow you to specify the style, width, and color of an element's border.
- An outline is a line drawn outside the element's border. both have same kind of properties ie. border-style; border-width, outline-style; outline-width

```html
<!DOCTYPE html>
<html>
<head>
<style>
p.dotted {border-style: dotted;}
p.dashed {border-style: dashed;}
p.solid {border-style: solid;}
p.double {border-style: double;}
p.groove {border-style: groove;}
p.ridge {border-style: ridge;}
p.inset {border-style: inset;}
p.outset {border-style: outset;}
p.none {border-style: none;}
p.hidden {border-style: hidden;}
p.mix {border-style: dotted dashed solid double;}
</style>
</head>
<body>

<h2>The border-style Property</h2>
<p>This property specifies what kind of border to display:</p>

<p class="dotted">A dotted border.</p>
<p class="dashed">A dashed border.</p>
<p class="solid">A solid border.</p>
<p class="double">A double border.</p>
<p class="groove">A groove border.</p>
<p class="ridge">A ridge border.</p>
<p class="inset">An inset border.</p>
<p class="outset">An outset border.</p>
<p class="none">No border.</p>
<p class="hidden">A hidden border.</p>
<p class="mix">A mixed border.</p>

</body>
</html>



```
### CSS Variable

```css

/* Global varibale in :root*/
:root {
  --main-bg-color: brown;
}

/* Local variable for this file level access */
body {
    --nav-width: 200px;
    margin: 0 0 0 var(--nav-width);
    font-family: 'Quicksand', sans-serif;
    font-size: 18px;
}

.nav {
    position: fixed;
    top: 0;
    left: 0;
    width: var(--nav-width);
    height: 100vh;
    background: #222222;
}

.nav__link {
    display: block;
    padding: 12px 18px;
    text-decoration: none;
    color: #eeeeee;
    font-weight: 500;
}

.nav__link:hover {
    background: rgba(255, 255, 255, 0.05);
}

#app {
    margin: 2em;
    line-height: 1.5;
    font-weight: 500;
}

a {
    color: #009579;
}

````

### Margin and Padding
- The CSS margin properties are used to create space around elements, outside of any defined borders.
- Padding is used to create space around an element's content, inside of any defined borders.

```css
div {
  padding-top: 50px;
  padding-right: 30px;
  padding-bottom: 50px;
  padding-left: 80px;
}

p {
  margin: 25px 50px 75px 100px;
}
/* property with two values*/
p {
  margin: 25px 50px;
}
/* property with three values*/
p {
  margin: 25px 50px 75px;
}

```

### The CSS Box Model
In CSS, the term "box model" is used when talking about design and layout. The CSS box model is essentially a box that wraps around every HTML element. It consists of: margins, borders, padding, and the actual content. The image below illustrates the box model:

Explanation of the different parts:

- Content - The content of the box, where text and images appear
- Padding - Clears an area around the content. The padding is transparent
- Border - A border that goes around the padding and content
- Margin - Clears an area outside the border. The margin is transparent
```css
div {
  width: 300px;
  border: 15px solid green;
  padding: 50px;
  margin: 20px;
}
```

### Text CSS

```css

div {
  border: 1px solid gray;
  padding: 8px;
}

h1 {
  text-align: center;
  text-transform: uppercase;
  color: #4CAF50;
}

p {
  text-indent: 50px;
  text-align: justify;
  text-align-last: right
  letter-spacing: 3px;
}

a {
  text-decoration: none;
  color: #008CBA;
}

p {
text-shadow: 2px 2px 4px red;
letter-spacing: 5px;
line-height: 1.8;
text-indent: 50px; /*indentation of the first line of a text*/
word-spacing: 10px;
direction: rtl;
text-align-last: justify;
text-decoration-line: overline underline;
text-decoration-color: red;
text-transform: uppercase;
}

```

### Font - Google Fonts

Best Web Safe Fonts for HTML and CSS

- Arial (sans-serif)
- Verdana (sans-serif)
- Helvetica (sans-serif)
- Tahoma (sans-serif)
- Trebuchet MS (sans-serif)
- Times New Roman (serif)
- Georgia (serif)
- Garamond (serif)
- Courier New (monospace)
- Brush Script MT (cursive)

```html
<head>

 <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Audiowide|Sofia|Trirong|Abril+Fatface|Poppins&effect=fire|neon|outline|emboss|shadow-multiple"
    />
<style>
  h1 {
font-family: cursive;
font-style: italic;
font-weight: bold;
font-size: 40px;
}
h1.a {font-family: "Audiowide", sans-serif;}
h1.b {font-family: "Sofia", sans-serif;}
h1.c {font-family: "Trirong", serif; text-shadow: 3px 3px 3px #ababab;}
</style>
</head>
<body>
<h1 class="font-effect-fire">My Company</h1>
</body>
```
### Google Material Icons

```html
<!DOCTYPE html>
<html>
  <head>
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/icon?family=Material+Icons"
    />
  </head>
  <body>
    <i class="material-icons">cloud</i>
    <i class="material-icons">favorite</i>
    <i class="material-icons">attachment</i>
    <i class="material-icons">computer</i>
    <i class="material-icons">traffic</i>
  </body>
</html>

```

### Link and states

```html
<style>
/* unvisited link */
a:link {
  color: red;
}

/* visited link */
a:visited {
  color: green;
}

/* mouse over link */
a:hover {
  color: hotpink;
}

/* selected link */
a:active {
  color: blue;
}
</style>
```


### Ordered and Unorderd List

```html
<style>
      ul {
        background: #3399ff;
        padding: 20px;
        list-style-image: url("sqpurple.gif");
      }
      ul li {
        list-style-position: outside|inside;
        list-style-type: circle|square|upper-roman|lower-alpha;
        background: #ffe5e5;
        color: darkred;
        padding: 5px;
        margin-left: 35px;
      }
</style>
```


### Table CSS

```html
<!DOCTYPE html>
<html>
  <body style="font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;">
    <style>
      table {
        border-collapse: collapse;
        border: 1px solid grey;
        width: 100%;
      }
      th {
        background-color: #04aa6d;
        color: white;
        height: 10px;
        padding: 15px;
        border: 1px solid grey;
        border-bottom: 1px solid #ddd;
      }
      td {
        border-bottom: 1px solid #ddd;
        height: 10px;
        border: 1px solid grey;
        vertical-align: bottom;
        padding: 5px;
      }
      tr:hover {
        background-color: lightgray;
      }
      tr:nth-child(even) {
        background-color: #f2f2f2;
      }
    </style>
    <div style="overflow-x: auto;">
      <table>
        <tr>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Points</th>
          <th>Points</th>
          <th>Points</th>
        </tr>
        <tr>
          <td>Jill</td>
          <td>Smith</td>
          <td>50</td>
          <td>50</td>
          <td>50</td>
        </tr>
        <tr>
          <td>Eve</td>
          <td>Jackson</td>
          <td>94</td>
          <td>94</td>
          <td>94</td>
        </tr>
        <tr>
          <td>Adam</td>
          <td>Johnson</td>
          <td>67</td>
          <td>67</td>
          <td>67</td>
        </tr>
      </table>
    </div>
  </body>
</html>

```


