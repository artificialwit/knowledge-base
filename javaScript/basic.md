# JavaScript basics
  Java script basic contains the basic programming details. Use reference link to go for basic understanding. and that summary is written.

## References
  - https://github.com/Asabeneh/30-Days-Of-React/blob/master/01_Day_JavaScript_Refresher/01_javascript_refresher.md
  - (Date and Time Library)[https://date-fns.org]
  

## Setup
  - You may need to install these extensions from Visual Studio Code
    - Prettier
    - ESLint
    - Bracket Pair Colorizer
    - ES7 React/Redux/GraphQL/React-Native snippets
    - Live server - once install right click on .html and use open with live server

## Console Functions
  - console.log('Pratul', 'Chandra' , 'Dwivedi' ,)
  - console.time('mytimer')
  - console.timeEnd('mytimer')
  - console.table(data)
  - console.clear()
  - console.assert(i>2)
  - console.info('data is saved.')
  - console.log(3 ** 2) // Exponentiation 3 ** 2 == 3 * 3

## Variable
variable - We use var, let and const to declare a variable. The var is functions scope, however let and const are block scope. In this challenge we use ES6 and above features of JavaScript. Avoid using var

## Array
Array in JS - Array is a class and can use its constructor - const arr = Array(), Or let arr= []

## Loop

## Script

JavaScript can be added to a web page in three different ways:
- Inline script - <button onclick="alert('Welcome to 30DaysOfJavaScript!')">Click Me</button>
- Internal script - can be written in the head or the body  
- External script - <script src="introduction.js"></script>
- Multiple External scripts - 

### Export and Import 

#### References
https://javascript.info/import-export

#### Export before declarations
```js
// export an array
export let months = ['Jan', 'Feb', 'Mar','Apr', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];

// export a constant
export const MODULES_BECAME_STANDARD_YEAR = 2015;

// export a class
export class User {
  constructor(name) {
    this.name = name;
  }
}

// export class as default class
export default class User { // just add "default"
  constructor(name) {
    this.name = name;
  }
}

// if i dont put export keyword in front of class/function/variable
function sayHi(user) {
  alert(`Hello, ${user}!`);
}

function sayBye(user) {
  alert(`Bye, ${user}!`);
}

export {sayHi, sayBye}; // a list of exported variables
//or 
export {sayHi as hi, sayBye as bye};
or 
// re-export the default export as User
export {default as User} from './user.js';

```
#### Import 
```js

import User from './user.js'; // not {User}, just User. When it is default expor

import {sayHi, sayBye} from './say.js';
sayHi('John'); // Hello, John!

// or
import {sayHi as hi, sayBye as bye} from './say.js';
hi('John'); // Hello, John!

// or 
import * as say from './say.js';
say.hi('John'); // Hello, John!

```

#### GET / POST Web Request 
Make sure when your import js file, use type="module"
```html
// index.html
<!DOCTYPE html>
<html>
  <head>
    <title>Artifial Wit</title>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="./src/styles.css" />
  </head>
  <body>
    <h1>Artifial Wit</h1>
    <ul></ul>
    <script type="module" src="src/index.js"></script>
  </body>
</html>


```
```js
// index.js

import { urls } from "./app_urls.js";

listEmployees();

async function listEmployees() {
  let requestJsonData = {
    firstName: "Pratul"
  };
  let authToken = "asfaggagagagadgag";
  let responseJsonData = await httpRequest(
    urls.employees,
    "GET",
    authToken,
    requestJsonData
  );
  //console.log(responseData);
  if (responseJsonData.isSuccess) {
    responseJsonData.data.forEach((emp) => {
      let ul = document.querySelector("ul");
      let li = document.createElement("li");
      li.innerHTML = "<li>" + emp.firstName + " " + emp.lastName + "</li>";
      ul.appendChild(li);
    });
  }
}

async function httpRequest(url, methodType, authToken, requestJsonData) {
  let myHeaders = new Headers();

  // in case of auth request
  if (authToken !== "") {
    myHeaders.append("Authorization", "Bearer " + authToken);
  }

  let requestOptions;

  if (methodType === "GET") {
    requestOptions = {
      method: methodType,
      headers: myHeaders
      //body: requestData // "GET method cannot have body, so use only when method type is POST"
    };
  }
  if (methodType === "POST") {
    myHeaders.append("Content-Type", "application/json");
    requestOptions = {
      method: methodType,
      headers: myHeaders,
      body: JSON.stringify(requestJsonData)
    };
  }

  let responseData = await fetch(url, requestOptions)
    .then((res) => res.text())
    .then((data) => {
      let responseData = JSON.parse(data);
      console.log(responseData.message, " Url is : ", url);
      return responseData;
    })
    .catch((err) => console.log("Error : ", url, " : " ,err));

  return responseData;
}


```

```js
// app_urls.js
export const urls = {
  employees: "data/employees.json"
};

```

```js
// data/employees.json

{
  "isSuccess": true,
  "message": "Request is successfully executed.",
  "statusCode": 200,
  "data": [
    { "firstName": "Pratul", "lastName": "Dwivedi" },
    { "firstName": "Manish", "lastName": "Adwani" },
    { "firstName": "Karam", "lastName": "Sharma" }
  ]
}

```




