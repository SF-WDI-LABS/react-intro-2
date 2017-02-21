<img src="https://cloud.githubusercontent.com/assets/6520345/23081189/8962462e-f508-11e6-88f1-4a3fa2ddca99.png" alt="cog" width= "50px"/>
# Intro to React.js: Part 2

---

![react-logo](./images/react-white-logo.png)

---

## Learning Objectives
Developers will be able to:

* Pass in data to a React component via `props`.
* Modify the `state` of a React component through events.

### Intro

Before our break, we learned that React is a powerful and efficient front-end framework that emphasized performance and reusability of _components_, and that it utilizes _JSX_ for these components. This is what we had for our `Hello` component:

```js
// bring in React and Component instance from react
import React, {Component} from 'react'

// define our Hello component
class Hello extends Component {
  // what should the component render
  render () {
    // Make sure to return some UI
    return (
      <h1>Hello World!</h1>
    )
  }
}

export default Hello
```

Now we'll see what we can do to make this more practical, and introduce the React concepts of `props` and `state`.

### Hello World: A Little Dynamic

Our `Hello` component isn't too helpful. Let's make it more interesting.
* Rather than simply display "Hello world", let's display a greeting to the user.
* So the question is, how do we feed a name to our `Hello` component without hardcoding it into our render method?

First, we pass in data wherever we are rendering our component, in this case in `src/index.js`:

```js
import ReactDOM from `react-dom`
import Hello from './App.js'

ReactDOM.render(
  <Hello name={"Nick"} />,
  document.getElementById('root')
)
```

Then in our component definition, we have a reference to that data via as a property on the `props` object...

```js
class Hello extends Component {
  render () {
    return (
      <h1>Hello {this.props.name}</h1>
    )
  }
}
```

In the above example, we replaced "world" with `{this.props.name}`.

#### What are `.props`?

Properties! Every component has `.props`
* Properties are immutable. That is, they cannot be changed while your program is running.
* We define properties in development and pass them in as attributes to the JSX element in our `.render` method.

First we can pass multiple properties to our component when its rendered in `src/index.js`..

```js
import ReactDOM from `react-dom`
import Hello from './App.js'

ReactDOM.render(
  <Hello name={"Nick"} age={24} />,
  document.getElementById('root')
)
```

Then in our component definition we have access to both values...

```js
class Hello extends Component {
  render () {
    return (
      <div>
        <h1>Hello {this.props.name}</h1>
        <p>You are {this.props.age} years old</p>
      <div>
    )
  }
}

```

> **NOTE:** The return statement in `render` can only return one DOM element. You can, however, place multiple elements within a parent DOM element, like we do in the previous example with `<div>`.

---


## State

So we know about React properties, and how they relate to our component's data.
* The thing is, `props` represent data that will be the same every time our component is rendered. What about data in our application that may change depending on user action?
* That's where `state` comes in...

Values stored in a component's state are mutable attributes.
* Like properties, we can access state values using `this.state.val`
* Setting up and modifying state is not as straightforward as properties. It involves explicitly declaring the mutation, and then defining methods to define how to update our state....

Lets implement state in our earlier `Hello` example by incorporating a counter into our greeting.

```js
class Hello extends Component {
  // when our component is initialized,
  // our constructor function is called
  constructor (props) {
    // make call to parent class' (Component) constructor
    super()
    // define an initial state
    this.state = {
      counter: 0 // initialize this.state.counter to be 0
    }
  }
  render () {
    return (
      <div>
        <h1>Hello {this.props.name}</h1>
        <p>You are {this.props.age} years old</p>
        <p>The initial count is {this.state.counter}
        </p>
      </div>
    )
  }
}
```

Ok, we set an initial state. But how do we go about changing it?
* We need to set up some sort of trigger event to change our counter.

<details>
  <summary><strong>
    Let's do that via a button click event. Where should we initialize it?
  </strong></summary>

  > In the return value of our Post's `render` method.

</details>

<!-- AM: Modify this question. They don't know that event listeners are passed in as attributes yet. -->

```js
class Hello extends Component {
  constructor (props) {
    super()
    this.state = {
      counter: 0
    }
  }
  handleClick (e) {
    // setState is inherited from the Component class
    this.setState({
      counter: this.state.counter + 1
    })
  }
  render () {
    // can only return one top-level element
    return (
      <div>
        <h1>Hello {this.props.name}</h1>
        <p>You are {this.props.age} years old</p>
        <p>The initial count is {this.state.counter}
        </p>
        <button onClick={(e) => this.handleClick(e)}>click me!</button>
      </div>
    )
  }
}
```

> Take a closer look at how this event is implemented. We use an attribute called `onClick` to define the behavior as to what happens when we click this particular button. As it's value, we're passing in an anonymous function that invokes handleClick, a function defined on this component.

Whenever we run `.setState`, our component "diff's" the current DOM, and compares the Virtual DOM node with the updated state to the current DOM.
* Only replaces the current DOM with parts that have changed.

---

## Closing

React, like Angular, is a powerful web framework that allows fast rendering and is a front-end tool. It works mainly in the "views" layer. It is meant to maintain readability, reusability, and performance.

### Additional Reading

* [Tyler McGinnis' React.js Program](http://www.reactjsprogram.com/)
* [Raw React: No JSX, Webpack, ES6, etc.](http://jamesknelson.com/learn-raw-react-no-jsx-flux-es6-webpack/)
* [Integrating React with Backbone](https://blog.engineyard.com/2015/integrating-react-with-backbone)
* [React DC (Meetup)](http://www.meetup.com/React-DC/)
* [React Tic-Tac-Toe (by Jesse Shawl)](https://github.com/jshawl/react-tic-tac-toe)


### What's Next?

* [Router](https://github.com/reactjs/react-router)
* [API/Axios](https://www.npmjs.com/package/axios)
* [Events](https://facebook.github.io/react/tips/dom-event-listeners.html)
* [Forms](https://facebook.github.io/react/docs/forms.html)

---
