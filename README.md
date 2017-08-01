# ![GA-Logo](https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67)Intro to React.js: Part 2



### Learning Objectives

* Pass in data to a React component via `props`.
* Modify the `state` of a React component through events using `setState`.
* Describe the setup of "downward data flow" that will allow components to share information and maintain a single idea about the state of the app.

### Intro

Before, we learned that React is a powerful and efficient front-end framework that emphasized performance and reusability of _components_, and that it utilizes _JSX_ for these components. This is what we had for our `Hello` component:

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

In the above example, we replaced `world` with `{this.props.name}`.

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



## State

So we know about React properties, and how they relate to our component's data.
* The thing is, `props` represent data that will be the same for the entire life of a given component. What about data in our application that may change depending on user action?
* That's where `state` comes in...

Values stored in a component's state are mutable attributes.
* Like properties, we can access state values, `val` for example, using `this.state.val`
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

Ok, we set an initial state. But in order to change the state, we need to set up some sort of trigger event.

<details>
  <summary><strong>
    Let's do that via a button click event. Where do you think should we initialize that button click event?
  </strong></summary>

  > Inside the `JSX` of our return value! In Hello `render` method we can instantiate our event listeners. Notice the ultra-slick ES6 function.

</details>


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

Whenever we run `.setState`, our component does a "diff", comparing the Virtual DOM node with the updated state to the current DOM. It only replaces the current DOM with parts that have changed.


## Closing

React, like Angular, is a powerful web framework that allows fast rendering and is a front-end tool. It works mainly in the "views" layer. It is meant to maintain readability, reusability, and performance.

### Additional Reading

* [Tyler McGinnis' React.js Program](http://www.reactjsprogram.com/)
* [Raw React: No JSX, Webpack, ES6, etc.](http://jamesknelson.com/learn-raw-react-no-jsx-flux-es6-webpack/)
* [Integrating React with Backbone](https://blog.engineyard.com/2015/integrating-react-with-backbone)
* [React Tic-Tac-Toe (by Jesse Shawl)](https://github.com/jshawl/react-tic-tac-toe)


### What's Next?

* [Router](https://github.com/reactjs/react-router)
* [API/Axios](https://www.npmjs.com/package/axios)
* [Events](https://facebook.github.io/react/tips/dom-event-listeners.html)
* [Forms](https://facebook.github.io/react/docs/forms.html)
