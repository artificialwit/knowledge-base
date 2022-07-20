# Advance

## Event Listener
 Event listner and event bubbling (from innermost to outermost), and event capturing (from outer most to inner most event). 
 if i want to remove a eventlister funciton, it must be named function. not annonymous function.

### References
https://www.youtube.com/watch?v=XF1_MlZ5l6M

### Index.html
```html
 <!DOCTYPE html>
<html>
  <head>
    <title>Js tutorial</title>
    <style>
      body {
        margin: 0;
        min-height: 100vh;
      }
      body,
      div {
        display: flex;
        justify-content: center;
        align-items: center;
      }
      .grandParent {
        width: 200px;
        height: 200px;
        background-color: red;
      }
      .parent {
        width: 130px;
        height: 130px;
        background-color: blue;
      }
      .child {
        width: 60px;
        height: 60px;
        background-color: green;
      }
    </style>
  </head>
  <body>
    <div class="grandParent">
      <div class="parent">
        <div class="child"></div>
      </div>
    </div>
    <script src="./index.js"></script>
  </body>
</html>

```

### Index.js

```js
const grandParent = document.querySelector(".grandParent");
const parent = document.querySelector(".parent");
const child = document.querySelector(".child");

grandParent.addEventListener(
  "click",
  (e) => {
    console.log("Grand parent 1 clicked.");
  },
  { once: true } // used to allowed this event listner only once
);

parent.addEventListener(
  "click",
  (e) => {
    e.stopPropagation(); // used to stop event bubbling and capturing(Tunnling)
    console.log("Parent is clicked");
  },
  { capture: true } // used for event capturing . by default it is false
);

child.addEventListener("click", printHi);

document.addEventListener("click", (e) => {
  console.log(e.target); // to get the object;
  console.log(
    "Document 1 clicked. will show all event bubbling events if i clicked on child (inner-most div)"
  );
});

// to remove a eventListner, must use a named fucntion not annonymius fuction.
setTimeout(() => {
  parent.removeEventListener("click", printHi);
}, 2000);
function printHi() {
  console.log("hi");
}
```

#### Example of how we can add event listner in all div using selector

```js
const divs = document.querySelectorAll("div");
divs.forEach((div) => {
  div.addEventListener("click", (e) => {
    console.log("hi");
  });
});

```

#### if i create a new div dynamically. then above eventlisnter will not be added.

```js
const newDiv = document.createElement("div");
newDiv.style.width = "200px";
newDiv.style.height = "200px";
newDiv.style.backgroundColor = "purple";
// i hv to add event listner again in this case
newDiv.addEventListener("click", () => {
  console.log("hi from new div");
});
document.body.append(newDiv);

#### let add listner from document and use matches seleciton

document.addEventListener("click", (e) => {
  if (e.target.matches("div")) {
    console.log("hi from document event listner for matching element");
  }
});
```

#### lets make a global event listner for all selected items.

```js
function addGlobalEventListner(type, selector, callback) {
  document.addEventListener(type, (e) => {
    if (e.target.matches(selector)) {
      callback(e);
    }
  });
}
addGlobalEventListner("click", "div", (e) => {
  console.log("hi from global event listner");
});

```

### Hoisting
Hoisting is JavaScript's default behavior of moving declarations to the top.
https://www.youtube.com/watch?v=EvfRXyKa_GI
whenever we use function or var keyword to create a variable or function in whole script. javascript basically moved that code on top of the script file.
that is called hoisting. thats why if i declare function after i called , it works. in case variable it is initialise with undefined. we cannot call arrow function before declaring it. that is major difference between arrow function and creating function using funciton keyword.
```js
// before

console.log(sum(2,3));
console.log(z);

var z=10;

function sum(a, b)
{
return a+b;
}

// after

var z=undefined;

function sum(a, b)
{
return a+b;
}
 z=10;
console.log(sum(2,3));

```

### PDF Viewer
```js
<!DOCTYPE html>
<html>
  <head>
    <title>PDF Viewer</title>
    <style>
      .pdfobject-container {
        height: 30rem;
        border: 1rem solid rgba(0, 0, 0, 0.1);
      }
    </style>
  </head>
  <body>
    <div id="pdfViewer"></div>
    <script src="./pdfobject.js"></script>
    <script>
      PDFObject.embed("SOP.pdf", "#pdfViewer");
    </script>
  </body>
</html>

```
