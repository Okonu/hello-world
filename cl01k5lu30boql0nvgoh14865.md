# Introduction to React and its components

This article is about the react introduction fundamentals that I made note of as I started learning React. It may not be as conclusive but it will give you some know-how.

## Virtual DOM

The most interesting and cool thing about react is that it makes the lives of UI developers really easy by the fact that it offers a virtual DOM.

The DOM(document object model) represents how things are rendered on the screen via the browser. While writing HTML code, each one of the HTML elements is nothing more than a sort of node within the tree-like structure. 

A virtual DOM is sort of an in-memory representation of the sort of actual DOM. As a react developer, one develops against a Virtual DOM and not the real DOM. This is because it is the responsibility of React to kind of take the changes that one has implemented and affected on the DOM and make sure the changes are applied to the real DOM. And that means that the actual logic of rendering things on screen is going to be the responsibility of React and not the developer. This means as a developer you don't have to be worried about how things are going to be rendered on the screen.


## React Components
React components are implemented as a Javascript class that has a state and a render method. 

**State:** data that you want to display when the component is rendered.

**Render:** responsible for describing what the UI should look like.

In React, changing the state of the component gives you a new react element. You don't have to work with the DOM element in browsers, you no longer have to write code to create and manipulate the DOM API or attach event handlers to DOM elements. 

You simply change the state of the component and React will automatically update the DOM toi match the state.
When the state changes, React reacts' to the state change and updates the DOM.


##React Vs Angular.

**React**   
- React is a library, it only takes care of the views and makes sure the view is in sync with the state.
thus a small API to learn 
- When using React we need to use other libraries like routing or calling HTTP services.

**Angular**
- Angular is a framework/complete solution
- Angular does not give you the chance to choose the libraries to work from

**N/B;** - Angular and React are similar in terms of the component-based architecture



 