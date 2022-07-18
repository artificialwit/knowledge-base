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

  - npm install n stable
  - npm install -g create-react-app
  - create-react-app myAppName
  - cd myAppName
  - npm start 


