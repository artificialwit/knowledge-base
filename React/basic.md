## React Basic

### References
- https://nodejs.org/en/download/
- https://www.npmjs.com/package/create-react-app

### 1. What is React?

React is a JavaScript library for building a reusable user interface(UI). The official React documentation can be found [here](https://reactjs.org/docs/getting-started.html). When we work with React we do not interact directly with the DOM. React has its own way to handle the DOM(Document Object Model) manipulation. React uses its virtual DOM to make new changes and it updates only the element, that needs changing. Do not directly interact with DOM when you build a React Application and leave the DOM manipulation job for the React virtual DOM. 

To summarize:

- React was released in May 2013 created by Facebook
- React is a JavaScript library for building reusable user interfaces / components
- React is used to build single page applications - An application which has only one HTML page.

### Prerequisite:
- Node is a JavaScript runtime environment that allows JavaScript to run on the server. Node was created in 2009. Node has played a great role for the growth of JavaScript. The React application starts by default at localhost 3000. The create-react-app has configured a node server for the React Application. That is why we need node and node modules

  - npm install n stable // run to get updated npm
  - npm install -g create-react-app // install react module using npm command globaly
  - create-react-app myAppName // create a react app with some basic file
  - cd myAppName // move to folder created by create-react-app command
  - npm start  // to start development server
  - npm run build // creates a build directory with a production build of your app


### React using js reference library

Babel will transpile the react JSX to pure JavaScript on the browser. In JSX element we write className instead of class because class is a reserved word in JavaScript. Similar to className, htmlFor instead of for in label tag. To inject data to a JSX we use the {} bracket

```html
https://reactjs.org/docs/getting-started.html
<body>
    <div class="root"></div>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/babel">
      // our code goes here
    </script>
  </body>
```

### Module 
- A single or multiple functions, that can be exported and imported when needed, can be included in a project. In React we do not use link to access modules or packages. 
- React and ReactDOM we need babel to transpile the JSX to JavaScript code. The ReactDOM package has a method render. The render method takes two arguments:a JSX element or a component and the root document.
- A Package is a module or a collection of modules. For instance, React, ReactDOM are packages.
- NPM was created in 2010. You do not need to install NPM separately - when you install node you will have also NPM. NPM is a default package manager for Node.js. It allows users to consume and distribute JavaScript modules that are available in the registry. NPM allows to create packages, use packages and distribute packages
- React allows us to write JSX and ReactDOM to render the JSX on the DOM
- React component is made of JavaScript functions or classes. A React component is a small, reusable code, which is responsible for one part of the application UI.Components can be:
  - Functional Component / Presentational Component / Stateless Component / Dumb Component
  - Class Component / Container Component/ Statefull Component / Smart Component





