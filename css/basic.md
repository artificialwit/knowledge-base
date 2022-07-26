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
